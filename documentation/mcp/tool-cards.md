# Tool cards

One short card per tool. Card format:

> **Purpose** — what it does, in one line, written for an LLM consumer.
> **Inputs** — typed parameters and what they mean.
> **Output** — JSON shape the LLM will see.
> **Gotchas** — edge cases / common failure modes.

Every tool's return value is a typed Pydantic v2 `BaseModel` defined in
[`models.py`](../models.py); FastMCP emits the schema as MCP 2025-06-18
*structured output*. The JSON shapes documented in the **Output** sections
below are exactly what an MCP client receives in `structuredContent`. The
existing `_provenance` block flows through every success model via
`extra="allow"`. Error returns share a single `ToolError` envelope:
`{ok: false, error, tool, [input]}`.

---

## `ping`

**Purpose**: Sanity-check that the server is reachable and list the
tools that are planned/implemented.
**Inputs**: none.
**Output**: `{ok, server, version, tools_planned}`.
**Gotchas**: none.

---

## `validate_uniprot`  ✅ Week 2

**Purpose**: Resolve any UniProt-ish input (accession or gene name) to a
canonical, existing UniProt entry. Call this BEFORE any tool that
takes a UniProt accession — it's the anti-hallucination gate.
**Inputs**:
  - `query: str` — accession (e.g. `P04637`, `P04637-1`) or gene name (e.g. `TP53`, `p53`, `BRCA1`). Case-insensitive.
  - `organism_id: int | None = None` — NCBI taxon id to disambiguate gene names across organisms. Examples: `9606` human, `10090` mouse, `559292` *S. cerevisiae* S288c. Omit for default human-first ranking.
**Output on success**: `{ok: true, input, accession, name, organism, taxon_id}`.
**Output on failure**: `{ok: false, input, error}`.
**Gotchas**:
  - Gene-name lookup uses `gene_exact:{q} AND reviewed:true` (Swiss-Prot only).
    With size=1 the UniProt search ranks weirdly (verified live 2026-05-07:
    `TP53 size=1` → Cricetulus, `TP53 size=10` → human). We always request
    size=10 internally and take results[0].
  - Accessions matching the regex (`P12345`, `Q00987`, etc.) go to direct
    lookup; everything else falls into the search path.
  - Isoform suffix (e.g. `P04637-1`) is preserved through to the lookup.
  - For non-human orthologs, **always pass `organism_id`** rather than relying
    on default ranking.

---

## `intact_search_interactors`  ✅ Week 2

**Purpose**: Free-text search of IntAct interactors (proteins, RNAs,
complexes, small molecules) when the user mentions something that isn't
a clean accession. Bridge from natural-language names to UniProt
accessions.
**Inputs**:
  - `query: str` — substring match against IntAct's interactor index. Be
    aware: `"p53"` matches both TP53 and unrelated entries containing
    "p53" (e.g. `P53350` = PLK1).
  - `species: str | None = None` — taxon id (e.g. `"9606"`), English alias
    (`"human"`, `"mouse"`, `"yeast"`, `"rat"`, `"fly"`, `"worm"`,
    `"zebrafish"`), or scientific-name substring (`"Homo"`,
    `"Saccharomyces"`). Filtering is **client-side** (the IntAct
    `ws/interactor` service has no server-side species filter, verified
    live 2026-05-07).
  - `max_results: int = 20` — page size. Total match count is reported
    in `total_elements` even if the page is truncated.
**Output**:
  ```
  {total_elements, returned, results: [{accession, name, description,
   species, taxon_id, kind, intact_ac}]}
  ```
**Gotchas**:
  - Returns non-protein entities (RNAs, complexes, ChEBI small molecules)
    if they match. Filter on `kind == "protein"` if only proteins matter.
  - Substring match means `"p53"` is noisy. Prefer the gene symbol
    (`"TP53"`) when known, or pre-validate with `validate_uniprot`.
  - For UniProt-specific resolution, prefer `validate_uniprot` first;
    use this tool only when the user mentions an entity by description.

---

## `intact_interactions`  ✅ Week 2 (`author` Week 7; filter expansion 2026-06)

**Purpose**: Get IntAct interactions for one protein, with rich server-side
filters. Every filter below is a real IntAct form-field, verified against the
live OpenAPI (`docs/verified-endpoints.md`). One enriched tool closes the
interaction-type, confidence-band, negative, expansion, host/cross-species,
mutation and self-interaction gaps (report items N5/N10/N11/N12 + Q1-3/Q5-8).
**Inputs**:
  - `accession: str` — canonical UniProt accession. Pre-validate with
    `validate_uniprot`. Can be `""` if `author` is set. Matched as **broad free
    text** by default (superset incl. isoforms — see `match` and Count scope).
  - `match: str = "broad"` — `"broad"` matches the accession as free text (the
    portal's DEFAULT search box; superset incl. isoforms). `"exact_id"` scopes to
    the canonical `id:` field (the portal's ADVANCED search; e.g. 288 vs broad 299
    for TP53 direct interactions). No-op with `advanced_query`/`feature_types`.
  - `min_miscore: float = 0.45` / `max_miscore: float | None` — MIscore band.
    e.g. `min=0.45, max=0.6` = medium-confidence only; `min=0.6` = high only.
  - `species: str | None` — participant species (`interactorSpeciesFilter`):
    taxon id, English alias (`"human"`), or scientific name.
  - `host_organism: str | None` — experimental host (`interactionHostOrganismsFilter`),
    taxon id preferred; for cross-species / host-background studies.
  - `detection_method: str | None` — `interactionDetectionMethodsFilter`,
    MI id preferred (`"MI:0018"` two hybrid, `"MI:0096"` pull down).
  - `interaction_type: str | None` — `interactionTypesFilter`, MI id
    (`"MI:0915"` physical association, `"MI:0407"` direct interaction).
  - `interactor_type: str | None` — `interactorTypesFilter`, MI id
    (`"MI:0326"` protein, `"MI:0328"` small molecule).
  - `author: str | None` — publication-author free-text (matched anywhere in
    publication metadata; IntAct has no first-author field).
  - `negative: str = "exclude"` — `"exclude"` (default, positives only),
    `"only"` (curated non-interactions, `NEGATIVE_ONLY`), or `"both"`.
  - `mutation_only: bool = False` — only interactions with a mutation feature
    (`mutationFilter`).
  - `expansion: str = "any"` — `"any"`, `"expanded"` (spoke/matrix only), or
    `"binary"` (exclude expanded — true binary evidence) (`expansionFilter`).
  - `intra_species_only: bool = False` — same-species only (`intraSpeciesFilter`);
    NOT the same as self-interaction.
  - `self_only: bool = False` — homodimers / self-association only (both
    participants the same molecule). **Client-side** post-filter on the page.
  - `max_results: int = 50` — page size; total in `total_elements`.
**Output**:
  ```
  {total_elements, returned, interactions: [{
    ebi_id, miscore,
    detection_method, detection_method_mi,
    interaction_type, interaction_type_mi,
    expansion_method, negative,
    a: {accession, database, name, species, taxon_id},
    b: {accession, database, name, species, taxon_id},
    pubmed_id
  }], filters_applied, count_scope_note?}
  ```
**Gotchas**:
  - Negative-evidence rows are **excluded by default** (`negative="exclude"`).
    Pass `negative="only"` for curated non-interactions.
  - **`self_only` and `expansion="binary"` are client-side filters** (IntAct has
    no server param for either; `expansionFilter=false` is a verified no-op). The
    tool paginates up to `scan_cap` (default 5000 — covers virtually every hub,
    e.g. APP's ~2800 binary) and reports the exhaustive
    post-filter count as **`matched`** (report THIS, not `total_elements`, which
    is the pre-filter server count), plus `scanned` and `truncated`. The
    `interactions` list is capped at `max_results`. For a pure server-side
    expanded count use `intact_facets(facet="expansion")`.
  - `interaction_type`/`interactor_type` expect **MI ids** (the styled facet
    `termId`), not labels.
  - **PMID:** pass a bare PMID as the `accession`/query — `total_elements` is then
    that publication's interaction count (report it; the `interactions` list is one
    page), and a `publication_query_note` says so + warns the match is free-text
    prefix (not exact; no structured pubid field). See `docs/verified-endpoints.md`.
  - Endpoint is `POST /ws/interaction/list` (DataTables-style; needs
    `draw=1` param or you get HTTP 400).
  - **Count scope (broad vs `id:`).** A plain `accession` is matched as **broad
    free text** — a SUPERSET of the portal's field-scoped `id:` count (it also
    matches isoforms `P04637-1/-2` and any field where the string appears). This
    equals the portal's **DEFAULT** search box; the smaller **ADVANCED** `id:`
    count (TP53: broad **299/874** vs `id:` **288/853** for MI:0407/MI:0915) comes
    from `match="exact_id"` or `advanced_query='id:P04637 AND type:"MI:0407"'`.
    Every broad result carries a `count_scope_note`. — Caveat on free-text mode:
    the bare `id:` prefix in plain `query` is ignored (returns 0 rows) **unless**
    `advancedSearch=true` is sent, which `match="exact_id"` and the `feature_types`
    path do (then `id:"P04637"` is exactly the scope). (Supersedes the older
    "`id:P04637` always returns 0" note, which described only free-text mode.)
  - For very high-degree hubs the page can be heavy; use `max_results=20`
    and rely on `total_elements` when only the count matters.
  - With `author`: `total_elements` is the count of interactions
    matching the free-text query anywhere in publication metadata, not
    the count of first-author papers.

---

## `intact_interaction_details`  ✅ Week 3

**Purpose**: Curatorial detail for one IntAct interaction by `EBI-xxxx`
id. Use after `intact_interactions` to drill into a specific evidence
for publication, cross-refs, or curator annotations.
**Inputs**: `ebi_id: str` — IntAct internal id, e.g. `"EBI-6974073"`.
**Output on hit**:
```
{found: true, ebi_id, short_label,
 interaction_type: {name, mi}, detection_method: {name, mi},
 host_organism: {name, taxon_id}, negative,
 publication: {pubmed_id, title, journal, authors[], date},
 xrefs: [{database, database_mi, identifier, url}, ...],
 annotations: [{topic, topic_mi, description}, ...],
 n_confidences, n_parameters}
```
**Output on miss**: `{found: false, ebi_id}` (IntAct returns 200 + empty
body for unknown ids — verified live 2026-05-07).
**Gotchas**:
  - This endpoint does **not** include the participating proteins. For
    "who interacts with whom" use `intact_interactions` instead — it
    already returns both participants per row.
  - For mutations / binding sites / features the sibling endpoints
    `/participants/details/{ac}` and `/features/details/{ac}` exist but
    are not yet wrapped by this server.
  - `confidences` and `parameters` arrays are usually empty in this
    endpoint; we report only their counts (`n_confidences`,
    `n_parameters`) to keep the payload small.

---

## `intact_features`  ✅ Week 7

**Purpose**: Curator-annotated features (binding regions, mutations,
tags) for one IntAct interaction by `EBI-xxxx` id. Use AFTER
`intact_interactions` to surface per-participant binding domains for
the Q2 tabular use-case.
**Inputs**: `ebi_id: str` — IntAct internal id, e.g. `"EBI-15565530"`.
**Output**:
```
{ebi_id, n_features,
 features: [{
   feature_ac,                 # IntAct internal id of this feature
   name,                       # e.g. "Region 94-312"
   type, type_mi,              # e.g. "sufficient to bind", "MI:0442"
   effect,                     # mutation effect or null (N7): decreasing/
                               # increasing/disrupting/no effect/complex/unspecified
   role, role_mi,              # may be None
   ranges,                     # list of strings, e.g. ["94-312"]
   participant_name,           # e.g. "p53_human"
   participant_accession,      # UniProt accession of the participant
   participant_database,       # e.g. "uniprotkb"
 }, ...]}
```
Optional input `effect_filter` keeps only mutation features with the given
effect (`"decreasing"`/`"increasing"`/`"disrupting"`/`"no effect"`). Pair with
`intact_interactions(..., mutation_only=True)` to study mutation effects (N7).
**Gotchas**:
  - The endpoint is paginated (Spring Pageable envelope) but we always
    request `pageSize=200`. If an interaction has >200 features (none
    seen in the wild — p53's richest interaction has 14), some will be
    truncated silently.
  - `n_features = 0` does NOT distinguish "interaction does not exist"
    from "interaction has no curated features" — both produce
    `content: []` (verified live 2026-05-10 with EBI-9999999999 vs
    EBI-6974073). Call `intact_interaction_details` separately if
    existence matters.
  - The richest p53 demo interaction is `EBI-15565530` (MDM2-p53
    peptide-array binding study, 14 `MI:0442` "sufficient to bind"
    regions). Most p53 evidences have 0 curated features.
  - `ranges` is a list of strings like `"94-312"` (some features span
    multiple ranges). The format is human-readable; LLM can quote
    directly in tabular output.
  - Sibling endpoint `/ws/graph/participants/details/{ac}` is currently
    broken on the live server (returns HTTP 500 with a Java NPE,
    verified 2026-05-10) — we do not use it.

---

## `intact_protein_features`  ✅ 2026-06 (composite; Q29/Q30/Q31)

**Purpose**: Curated features of a protein aggregated ACROSS all its
interactions — answers "which mutations decrease/disrupt X's interactions?" and
"which of X's interactions carry a 'binding site' / 'sufficient to bind'
feature?" without scanning each interaction by hand. Server-side bounded scan.
**Inputs**: `accession: str`; `feature_type: str | None` (`"MI:xxxx"` exact, else
substring on label); `effect: str | None` (decreasing/increasing/disrupting/
no effect/complex/unspecified); `min_miscore: float = 0.0`; `species: str | None`;
`max_interactions_to_scan: int = 500` (covers hubs like CFTR's ~380 mutation
interactions; `truncated=True` => distributions are over the scanned subset).
**Output**:
```
{seed, interactions_scanned, truncated, features_total, features_matched,
 effect_distribution:{disrupting, complex, "no effect", ...},
 type_distribution:{label:count},
 features:[{ebi_id, partner_accession, partner_name, feature_ac, name, type,
            type_mi, effect, role, ranges}], filters_applied}
```
**Gotchas**:
  - `effect` triggers a `mutation_only=True` scan (shrinks the candidate set).
  - **The distributions cover ALL the protein's features in the scanned set**,
    before the type/effect filter — so when `effect="decreasing"` returns
    nothing, `effect_distribution` still shows what IS curated (e.g. CFTR uses
    "disrupting"/"complex", not "decreasing"). Honest about `truncated`: the
    sample is the highest-MIscore interactions up to `max_interactions_to_scan`.
  - Composite: one `intact_interactions` + N `intact_features` under
    `Semaphore(8)`. From the LLM's perspective: one call.

---

## `intact_export_interaction`  ✅ 2026-06 (N9)

**Purpose**: Export one interaction as serialized MITAB / PSI-MI XML for
handoff to another pipeline. Endpoint confirmed live.
**Inputs**: `ebi_id: str` (e.g. `"EBI-6974073"`), `format: str = "miTab27"`
— one of `miTab25/26/27/28`, `miXML25/30`.
**Output**: `{ebi_id, format, content_type, content}` where `content` is the
raw serialized record (tab-separated MITAB or PSI-MI XML).
**Gotchas**:
  - Unknown `format` is rejected client-side (no HTTP call) with the valid
    list; the endpoint also 400s on bad formats.
  - `content` can be large (full miXML30 of a hub interaction is ~100 KB).
  - Endpoint: `GET /ws/graph/export/interaction/{ac}?format=`.

---

## IntAct query model (read before using `query`/`accession`)

The IntAct `ws/interaction/*` `query` field is FREE TEXT + wildcards (`*`)
only. Field-scoped syntax (`species:2697049`, `taxidA:9606`, `pubid:…`) is
silently ignored unless `advancedSearch=true` is also sent (verified 2026-06-24:
`species:2697049` → 0 without the flag, 8130 with it; `pubauth:gingras` → 90;
`taxidA:9606 AND taxidB:10090` → 6112). The two modes are mutually exclusive —
with `advancedSearch` on, a bare accession (`P04637`) matches nothing. So:

  - To **filter**, pass a structured param (`species`, `detection_method`, …),
    never a `field:value` query — these are the same Solr filters the portal's
    advanced search builds, and each is individually verified.
  - To get a species/method/type **breakdown** (incl. whole-organism interaction
    counts), use `intact_facets`, not a `species:` query.
  - The `advancedSearch=true` MIQL path is real but reached only through the
    named `advanced_query` param on `intact_interactions` — use it only for a
    field-scoped predicate with no structured equivalent.
  - **Broad vs `id:` count scope.** Because `query` is free text, a plain
    `accession` matches a SUPERSET of the portal's field-scoped `id:` count — it
    also picks up isoforms (`P04637-1/-2`) and any field with the string. This
    equals the portal's **DEFAULT** search box (TP53: **299/874** for
    MI:0407/MI:0915). The smaller portal **ADVANCED** `id:` count (**288/853**)
    is reached via `intact_interactions(match="exact_id")` or
    `advanced_query='id:P04637 AND type:"MI:0407"'`. Every plain-accession result
    (in `intact_interactions`, and accession-seeded `intact_facets`) carries a
    `count_scope_note`. The composite tools inherit the broad scope intentionally
    (they canonicalize partners, so isoforms fold together).

See `docs/verified-endpoints.md:22,30,36,65` for the underlying verification.

---

## `intact_facets`  ✅ 2026-06 (N4); generalized 2026-06-24

**Purpose**: Aggregated counts over a set of IntAct interactions — the portal's
facet sidebar. Use for "break down by method/type/organism" and for the MIscore
histogram, without paging every interaction. The set is defined by a free-text
`query` (a species name, keyword, gene, or accession; empty = whole database)
plus optional structured filters. WHOLE-set counterpart of one protein; for
database-wide totals (proteins/interactions counts) use `intact_statistics`.
**Inputs**: `query: str = ""`, `facet: str = "species"` (one of `species`,
`detection_method`, `interaction_type`, `interactor_type`, `host_organism`,
`mutation`, `expansion`, `negative`, `miscore`), `min_miscore: float = 0.0`,
and the structured filters `species`, `host_organism`, `detection_method`,
`interaction_type`, `interactor_type`, `negative`, `mutation_only`,
`intra_species_only` (same semantics as `intact_interactions`).
**Output**:
```
{facet, total, buckets: [{key, term_id, count}], count_scope_note?}   # sorted by count desc
```
**Gotchas**:
  - **Best route for "count by interaction type for protein X"**: one
    `intact_facets(query=X, facet="interaction_type")` returns every type bucket
    (MI:0407, MI:0915, …) at once — cheaper than two `intact_interactions` calls.
    These bucket counts use the same **broad free-text scope** as
    `intact_interactions` (a superset of the portal's `id:` count); an
    accession-seeded result carries a `count_scope_note`. For the portal's exact
    per-type count use `intact_interactions(match="exact_id", interaction_type=…)`.
  - **The email's "species id + facets" workflow**: to count a species'
    interactions, call `intact_facets(query="sars-cov-2", facet="species")` and
    read the SARS-CoV-2 (taxon 2697049) bucket — do NOT pass
    `query="species:2697049"` (free text, matches nothing). See the query-model
    callout above.
  - Empty `query` facets across all of IntAct (sent as match-all `*`).
  - Endpoint `POST /ws/interaction/findInteractionFacets` (verified 2026-06-08).
    The portal's styled facet keys (`detection_method_mi_styled`,
    `type_mi_identifier_styled`, `combined_species`, `intact_miscore`, ...)
    are mapped to the friendly `facet` names above.
  - For `species`, the upstream bucket count is `{all, intra}`; we surface the
    `all` count.
  - `facet="miscore"` is the score histogram (bucketed values); its bucket
    counts sum to the set's total interaction count.

---

## `intact_statistics`  ✅ 2026-06-24

**Purpose**: Database-wide IntAct content statistics — total proteins,
interactions, binary interactions, publications, experiments, organisms; species
coverage; detection-method distributions; and historical time series. Reads
IntAct's pre-computed statistics tables directly, so the LLM never needs to page
interactions or scrape the portal to count things. Whole-database counterpart to
`intact_facets` (which breaks down ONE query's interactions).
**Inputs**:
  - `section: str = "summary"` — `"summary"`, `"species_coverage"`,
    `"detection_methods"`, `"curation_history"`,
    `"publication_experiment_history"`, `"interactions_history"`.
  - `live_count: bool = False` — when true AND `section="summary"`, also fetch
    the live total binary-interaction count from `ws/interaction/countTotal`,
    returned as `live_binary_interaction_count`.
**Output**:
```
{section, source_file, columns: [str], rows: [dict], _provenance}
# + live_binary_interaction_count: int  (summary + live_count only)
```
Each `rows` item is one CSV row keyed by `columns`, numeric cells parsed to
numbers. For `"summary"` each row is `{Feature, Count}`.
**Gotchas**:
  - Statistics are periodic snapshots (not real-time). Only
    `live_binary_interaction_count` (opt-in) is live. The CSV's `Binary
    Interactions` row may lag and differ by one or two (e.g. 1787152 vs 1787151).
  - The `"summary"` `Feature` column carries an upstream typo, `"Interaction
    Dectection Methods"`; surfaced verbatim, not corrected.
  - Source is the `intact-portal-statistics` GitHub repo (`statistics_prod`
    branch) — a different backend from `ws/*`; provenance `upstream` is
    `"intact-portal-statistics"`.
  - `species_coverage` returns all ~11 major species; no per-organism filter.

---

## `intact_network`  ✅ 2026-06 (N1)

**Purpose**: First-shell interaction network of a protein — every neighbour
(node) and every interaction among them (edge). For network views and
shared-neighbour analysis (intersect two networks' node sets).
**Inputs**: `accession: str`, `min_miscore: float = 0.4`, `max_edges: int = 500`.
**Output**:
```
{seed, seed_accession, n_nodes_total, n_edges_total, n_nodes, n_edges,
 truncated, min_miscore,
 nodes: [{accession, name, type, taxon_id}],
 edges: [{source, target, miscore, interaction_type, detection_method,
          ebi_id, pubmed_id}]}
```
**Gotchas**:
  - Resolves the UniProt accession to its internal interactor AC via
    `findInteractor` first, then `POST /ws/graph/network/data`
    (`neighboursRequired=true`).
  - A hub's raw network is multi-MB (p53 ≈ 4.8 MB); edges are filtered by
    `min_miscore`, sorted by score, and capped at `max_edges` — raise the
    floor or lower the cap for big hubs. `truncated` flags the cap.
  - Two-shell (N2) is intentionally not implemented (a hub's first shell is
    already thousands of edges); call the tool on a neighbour to go deeper.

---

## `intact_complex`  ✅ 2026-06 (N6)

**Purpose**: Find Complex Portal complexes containing a protein, or get one
complex's full subunit composition + stoichiometry + function. Separate EBI
service (`complex-ws`), shared data model.
**Inputs**: `accession: str | None` (UniProt/gene/free text to search by),
`complex_ac: str | None` (e.g. `"CPX-7967"` for a direct lookup),
`max_results: int = 25`. Provide one.
**Output (search)**: `{mode:"search", query, size, returned, complexes:
[{complex_ac, name, organism, description, predicted}]}`.
**Output (details)**: `{mode:"details", complex_ac, name, species, function,
n_participants, participants:[{accession, name, stoichiometry, bio_role, type,
type_mi}], diseases, ligands}`.
**Gotchas**:
  - `complex_ac` takes precedence over `accession`; supply neither → in-band
    error.
  - Endpoints `GET /complex-ws/search/{q}` and `/complex-ws/complex/{cpx}`
    (verified live 2026-06-08).

---

## `intact_interactor_details`  ✅ 2026-06 (N8)

**Purpose**: The IntAct-side record for one molecule (name, type, species,
internal interactor AC). IntAct has no interactor-detail endpoint, so this
resolves via the search index and returns the best match.
**Inputs**: `accession: str` — UniProt accession or IntAct AC (`EBI-xxxx`).
**Output (hit)**: `{found:true, accession, name, description, species,
taxon_id, kind, intact_ac}`. **(miss)**: `{found:false, accession}`.
**Gotchas**: thin wrapper over `findInteractor` — for a list of candidates use
`intact_search_interactors`; this returns the single exact match.

---

## `disprot_disorder`  ✅ Week 3 (region detail enriched 2026-06, N14)

**Purpose**: DisProt CURATED disorder annotation for a UniProt accession,
with full region-level detail (boundaries, IDPO/GO term, ECO method, binding
partner, PDB cross-refs).
**Inputs**: `accession: str` — canonical UniProt accession.
**Output on hit**:
```
{found: true, accession, disprot_id, name, organism, taxon_id, length,
 dataset, genes, disorder_content,
 regions: [{region_id, start, end, term, term_id, term_ontology, namespace,
 evidence_code, evidence_name, interaction_partner?, cross_refs?}],
 n_regions, released}
```
**Output on miss**: `{found: false, accession}`.
**Gotchas**:
  - `interaction_partner` (UniProt id of a binding partner) and `cross_refs`
    (PDB) appear only on regions where they were curated.
  - `alphafold_very_low_content` is **not** exposed by the DisProt API
    (verified 2026-06-08) — the AlphaFold-vs-DisProt discrepancy use-case
    cannot be answered from this source.
  - Only ~3,200 proteins covered (live count 3199 on 2026-05-07). Most
    queries will return `found: false`; that's expected — the headline
    composite tool simply skips partners DisProt doesn't curate.
  - Endpoint is the simple `GET /api/{accession}` direct lookup, not
    `/api/search` (which doesn't actually filter by `accession=` param;
    the working filter param is `acc=`, but direct lookup is simpler).
  - DisProt returns HTTP 404 with a `{status: "not-exist"}` body for
    unknown accessions — we map that to `{found: false}`.
  - `disorder_content` is the fraction of residues curated as disordered
    (0..1); cited threshold for "substantially disordered" is ≥ 0.30.

---

## `disprot_search`  ✅ 2026-06 (N13/N15/N16/N17)

**Purpose**: The single search surface over DisProt — by organism / name /
dataset, by IDPO structural-state/transition term, by ECO experimental method,
or by GO function. Filters AND-combine.
**Inputs** (all optional, supply ≥1): `name`, `organism`, `ncbi_taxon_id`,
`dataset`, `release` (per-release snapshot tag, e.g. `"2021_12"`), `idpo_id`
(e.g. `"IDPO:0000011"` disorder→order), `eco_id` (e.g. `"ECO:0006206"`), `go_id`
(e.g. `"GO:0003723"` RNA binding), `acc`, `max_results=50`.
**Output**:
```
{size, returned, results: [{accession, disprot_id, name, organism, taxon_id,
 disorder_content, n_regions, dataset, released}], filters_applied}
```
**Gotchas**:
  - The working ontology-filter param names are `idpo_id`/`eco_id`/`go_id`
    — the report's `term_id`/`ec_id`/`namespace` are silently ignored by
    DisProt and return the whole DB (verified 2026-06-08).
  - `/search` returns FULL entries (heavy); results are a light summary capped
    at `max_results`, with the full count in `size`.
  - Calling with no filter is an in-band error (would return all 3,199).
  - Combine `idpo_id` (disorder→order) with `go_id` (binding) to approximate
    MoRF / binding-on-folding discovery (report Q40).
  - The per-release filter is the **singular `release`** — the plural `released`
    is a silent no-op (returns the whole DB; gold curation Q53, 2026-06-09).

---

## `disprot_release_compare`  ✅ 2026-06 (N19, composite)

**Purpose**: Diff two DisProt releases — which entries / regions were added or
removed between them. Closes report N19 (release comparison), which earlier
verification wrongly thought impossible (it tested the no-op plural `released`).
**Inputs**: `release_a: str`, `release_b: str` (tags, e.g. `"2021_12"`,
`"2022_06"`), `scope: "regions"|"entries" = "regions"`, `max_examples=20`.
**Output**:
```
{release_a, release_b, scope, entries_a, entries_b, regions_a, regions_b,
 n_added, n_removed, net, added_examples, removed_examples}
```
**Gotchas**:
  - Each snapshot is fetched via the **singular** `/search?release=<tag>` (the
    plural `released` is a no-op). Entries diffed by `disprot_id`, regions by
    `disprot_id:region_id` (region_id is per-entry-local).
  - Counts **all** curated regions (any structural state/function), not only
    IDPO 'disorder' — inspect `added_examples` to scope to a term.
  - Two full-DB snapshots are downloaded (~15 MB each) → a few seconds per call.

---

## `disprot_batch`  ✅ 2026-06 (N18, composite)

**Purpose**: Disorder lookup for a LIST of accessions in one call, with
server-side concurrent fan-out (`Semaphore(8)`). Prefer over many
`disprot_disorder` calls for a set of proteins.
**Inputs**: `accessions: list[str]` (isoform suffixes stripped, de-duped,
capped at 200), `min_disorder_content: float | None`.
**Output**:
```
{n_input, n_found, returned, entries: [{accession, disprot_id, name, organism,
 taxon_id, disorder_content, n_regions}]}
```
with not-curated accessions in `_provenance.missing`.
**Gotchas**:
  - Not-curated / hallucinated accessions are flagged in `_provenance.missing`,
    never errored (the call still succeeds). Pre-validate with `validate_uniprot`.
  - `min_disorder_content` excludes found-but-below-threshold entries from
    `entries` (they still count in `n_found`).

---

## `disprot_list_ids`  ✅ 2026-06 (N22)

**Purpose**: Enumerate all DisProt IDs (~3,200) — a utility/enumeration seed.
Most queries should use `disprot_search` instead.
**Inputs**: `limit: int | None`.
**Output**: `{total, returned, disprot_ids: ["DP00003", ...]}`.

---

## `disprot_statistics`  ✅ 2026-06 (N20, composite)

**Purpose**: Aggregate disorder statistics over a DisProt population — e.g.
"mean disorder content of all human entries". Composite over `disprot_search`.
**Inputs**: one of `ncbi_taxon_id` / `organism` / `dataset` (required),
`max_scan: int = 2000`.
**Output**: `{entry_count, sample_size, sampled, region_count,
mean_disorder_content, min_disorder_content, max_disorder_content,
filters_applied}`.
**Gotchas**:
  - `sampled=true` when the population exceeds `max_scan` — stats then describe
    the scanned sample, not the full population.
  - For release-over-release comparison (report N19) use `disprot_release_compare`
    — it filters via the singular `/search?release=` (the plural `released` is a
    no-op).

---

## `disordered_interactions`  ✅ Week 4 — HEADLINE

**Purpose**: COMPOSITE — high-confidence interactions of a protein where
at least one participant is substantially disordered (DisProt-curated).
This is the IDPfun2 raison d'être query.
**Inputs**:
  - `accession: str` — canonical UniProt accession.
  - `min_miscore: float = 0.45` — IntAct confidence threshold.
  - `min_disorder_content: float = 0.30` — disorder fraction threshold.
  - `species: str | None`, `detection_method: str | None`, `max_results: int = 50`
    — passed through to `intact_interactions`.
  - `aggregate_by_partner: bool = True` — default unit of answer is one
    row per unique UniProt partner (`mode: "by_partner"`); set to `False`
    for the legacy row-per-evidence behaviour (`mode: "by_evidence"`).
    Confirmed by HH 2026-05-08 ("dedup is preferable").
**Output (aggregate_by_partner=True, default)**:
```
{mode: "by_partner",
 evidences_in_intact, evidences_scanned,
 partners_unique, partners_queried, partners_with_disorder_data,
 partners_qualifying, partners_returned, results_truncated,
 partners: [{partner_accession, best_evidence, disorder_a, disorder_b}],
 thresholds: {min_miscore, min_disorder_content}}
```
**Output (aggregate_by_partner=False)**:
```
{mode: "by_evidence", total_input, total_output,
 interactions: [{...intact_interactions row..., disorder_a, disorder_b}],
 thresholds: {min_miscore, min_disorder_content},
 n_partners_queried, n_partners_with_disorder_data}
```
where `disorder_a` / `disorder_b` is `None` or `{source: "disprot",
disorder_content, disprot_id, n_regions}`. MobiDB integration was
removed 2026-05-08 at supervisor direction; only DisProt-curated
disorder is consulted.
**Gotchas**:
  - Implemented server-side to avoid N+1 round-trips through the LLM
    (a hub like p53 has hundreds of evidences for ~98 unique partners).
    Disorder lookups for distinct partners run concurrently via
    `asyncio.gather`.
  - In `by_partner` mode the composite scans up to `evidence_scan_limit`
    IntAct evidences (default 1000) to see the long tail of partners,
    then groups by canonical partner accession and keeps the best-MIscore
    evidence per partner. `max_results` truncates the **partners** list,
    sorted by best-MIscore desc; `results_truncated` flags when more
    qualifying partners exist beyond the cut.
  - Isoform suffixes (e.g. `P04637-1`) are canonicalized to the master
    accession (`P04637`) for the disorder lookup, since DisProt indexes
    by the master entry.
  - Non-protein participants (RNAs, complexes, ChEBI molecules) are
    skipped — they cannot have disorder content.
  - Negative-evidence rows are excluded by the underlying IntAct
    service by default.
  - The seed protein itself is treated as a participant for the disorder
    filter, so a homodimeric IDP can satisfy the query on its own.

## `feature_disorder_overlap`  ✅ Week 8 — Q9 closed

Stretch goal from the project spec (HH 2026-05-08 marked it as such):
overlap between IntAct curator-annotated features (binding regions,
mutations, tags) and DisProt-annotated disordered regions on the same
UniProt protein, on the same residue numbering.

**Inputs**:
  - `accession: str` — canonical UniProt accession.
  - `min_miscore: float = 0.45` — IntAct confidence threshold.
  - `max_interactions_to_scan: int = 50` — top-N high-confidence
    interactions to pull features from.

**Output**:
```
{seed,
 found_in_disprot, disprot_id, disorder_content,
 disprot_regions: [{start, end, term: "disorder"}],
 disprot_regions_raw_count,
 interactions_scanned, features_total,
 features_with_overlap, features_fully_disordered,
 features: [{ebi_id, feature_type, feature_type_mi, feature_role,
             feature_name, ranges, feature_length, overlap_residues,
             overlap_fraction, fully_disordered,
             overlapping_regions: [{region_start, region_end,
                                    overlap_start, overlap_end,
                                    overlap_length, term}]}],
 thresholds: {min_miscore, max_interactions_to_scan}}
```
On `found_in_disprot=False` every count is 0 and `features: []`. The
features list is sorted by `overlap_fraction` desc, then
`overlap_residues` desc.

**Gotchas**:
  - DisProt returns many region rows per accession (22 for SNCA, 63 for
    p53) with different evidence codes covering overlapping intervals.
    The composite filters to `term == "disorder"` and **merges into a
    sorted non-overlapping union** before intersection. Without this
    step a residue counted under N evidence codes would inflate
    `overlap_fraction` to N×.
  - `disprot_regions` in the output is the merged union;
    `disprot_regions_raw_count` keeps the raw row count for transparency.
  - Feature ranges are IntAct strings like `"94-312"`; `"?-?"` and other
    non-numeric forms skip silently.
  - Multi-range features (e.g. `["10-30", "50-70"]`) aggregate
    `overlap_residues` and `feature_length` across all ranges.
  - Server-side fan-out: one `disprot_disorder` call + one
    `intact_interactions` call + N `intact_features` calls under a
    `Semaphore(8)` cap. From the LLM's perspective: one tool call.
  - Live example: `feature_disorder_overlap("P37840")` for alpha-
    synuclein (fully disordered, DP00070) returns every feature with
    `overlap_fraction = 1.0`. `feature_disorder_overlap("P04637")` for
    p53 returns 7 features over 3 disorder spans (1-93, 291-312,
    361-393): TAD1 features (1-93, 1-52) fully disordered, DBD-spanning
    features (94-312) overlap ~10% with the 291-312 span.

---

## `enrichment_disorder`  ✅ 2026-06 (N24, composite) — IDPfun2 flagship

**Purpose**: Tests whether intrinsic disorder is ENRICHED among a protein's
high-confidence interaction partners, vs the organism's DisProt baseline.
Returns an enrichment ratio and an exact hypergeometric p-value — a question no
single API answers. This is the IDPfun2 thesis made executable.
**Inputs**: `accession: str`, `min_miscore: float = 0.6`,
`min_disorder_content: float = 0.30`, `background_taxon_id: int = 9606`.
**Output**:
```
{seed, n_high_conf_interactions, partners_truncated, n_partners,
 n_partners_assessed, n_disordered_partners, partner_disorder_rate,
 background_taxon_id, background_size, background_disordered, background_rate,
 enrichment_ratio, p_value, thresholds}
```
**Gotchas**:
  - Pipeline: `intact_interactions` (partners) → `disprot_batch` (which are
    DisProt-curated & disordered) → `disprot_search` (organism baseline) →
    ratio + hypergeometric (computed with `math.comb`, no scipy).
  - The FULL high-confidence partner set is scanned (up to 2000 interactions),
    not a single page — so the ratio is not skewed by truncation;
    `partners_truncated=True` flags the rare hub beyond the scan limit.
  - The background is the *curated DisProt set* for the organism, itself
    disorder-enriched by construction → the test is **conservative**. A ratio
    ~1 or <1 is a real result: disorder is NOT automatically enriched (e.g.
    human TP53 measures ratio ~0.8, p ~0.8 — not significant, gold 2026-06-09).
  - For a hub (TP53), the partner fan-out makes this the slowest tool
    (~2 min); raise `min_miscore` to shrink the partner set.
