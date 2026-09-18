# Using the IntAct–MCP tools

Use IntAct–MCP to find molecular interactions, examine their experimental evidence, and explore how they relate to
protein disorder annotations in DisProt. Once you have [connected your assistant](../user-guide/mcp.md), ask in ordinary
language. Your assistant chooses the tools; the names below help you recognise what it is using or request a specific
tool.

## Start with a question

Include the **protein and organism**, any **filters**, and the **output you want**. For example:

> Find interaction partners of human p53 with an IntAct confidence score (MIscore) of at least 0.6. Give me one row per
> partner, with the supporting IntAct identifiers and publications. Say whether the results are complete.

You can then build on the answer:

> Which of these interactions involve a protein with at least 30% of its sequence annotated as disordered in DisProt?
> Show which participant meets that threshold and identify proteins without DisProt annotations.

| What you want to do                                                                       | Tools to use                                                                     |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| [Identify a protein or molecule](#identify-a-protein-or-molecule)                         | `validate_uniprot`, `intact_search_interactors`, `intact_interactor_details`     |
| [Find interactions and examine the evidence](#find-interactions-and-examine-the-evidence) | `intact_interactions`, `intact_interaction_details`, `intact_export_interaction` |
| [Explore binding regions and mutations](#explore-binding-regions-and-mutations)           | `intact_features`, `intact_protein_features`                                     |
| [Explore networks and complexes](#explore-networks-and-complexes)                         | `intact_network`, `intact_complex`                                               |
| [Get counts and database summaries](#get-counts-and-database-summaries)                   | `intact_facets`, `intact_statistics`                                             |
| [Find protein disorder annotations](#find-protein-disorder-annotations)                   | `disprot_disorder`, `disprot_search`, `disprot_batch`                            |
| [Combine interaction and disorder evidence](#combine-interaction-and-disorder-evidence)   | `disordered_interactions`, `feature_disorder_overlap`, `enrichment_disorder`     |
| [Explore DisProt coverage and releases](#explore-disprot-coverage-and-releases)           | `disprot_statistics`, `disprot_release_compare`, `disprot_list_ids`              |
| [Check the connection](#check-the-connection)                                             | `ping`                                                                           |

## Identify a protein or molecule

### `validate_uniprot`

Use this first to confirm a protein's UniProt accession and organism before looking up its interactions or disorder
annotations. It accepts an accession such as `P04637`, an isoform accession, or a gene name such as `TP53`.

> Confirm the UniProt accession for mouse TP53 before searching for its interactions.

**Specify:** the protein name or accession (`query`) and organism (`organism_id`, for example `9606` for human or
`10090` for mouse). Always specify the organism for non-human proteins; the default lookup favours human results.

**You get:** the accession, protein name and organism, or a message that the input could not be resolved. Gene-name
searches use reviewed UniProt entries, so an unsuccessful search does not establish that the protein does not exist.

### `intact_search_interactors`

Use this when you have a name or description and want to find matching molecules in IntAct. It can find proteins, RNAs,
complexes and small molecules.

> Search IntAct for human molecules matching TP53 and show their identifiers and molecule types.

**Specify:** a search term (`query`), optionally a `species`, and the number of results to show (`max_results`, default
20). Species can be a taxon identifier, a common name such as `human`, or a scientific name.

**You get:** matching names, identifiers, organisms and molecule types. Searches match parts of text, so check the
identity of each result. For a known protein or gene symbol, use `validate_uniprot` to resolve its UniProt accession.

### `intact_interactor_details`

Use this to inspect IntAct's record for a molecule you have already identified.

> Show the IntAct record for P04637, including its molecule type, organism and IntAct identifier.

**Specify:** a UniProt accession or IntAct molecule identifier (`accession`).

**You get:** its name, description, organism, molecule type and IntAct identifier, or an indication that no match was
found. Use `intact_search_interactors` if you need a list of candidates.

## Find interactions and examine the evidence

### `intact_interactions`

Use this to find interactions for a protein and narrow the evidence by confidence, organism or experiment.

> Find human p53 interactions supported by pull-down experiments, with MIscore at least 0.6. Show both participants,
> the detection method, IntAct interaction identifier and publication for each result.

**Specify:** a validated UniProt `accession` and the filters relevant to your question:

| Choice                      | Parameter and behaviour                                                                                                |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------|
| Confidence range            | `min_miscore` (default `0.45`) and optional `max_miscore`                                                              |
| Participant organism        | `species`                                                                                                              |
| Experimental host organism  | `host_organism`; this is separate from the participants' species                                                       |
| Detection method            | `detection_method`, preferably an MI identifier such as `MI:0096` for pull down                                        |
| Interaction type            | `interaction_type`, such as `MI:0407` for direct interaction or `MI:0915` for physical association                     |
| Molecule type               | `interactor_type`, such as `MI:0326` for protein                                                                       |
| Curated negative evidence   | `negative="only"`; the default `"exclude"` returns positive evidence, while `"both"` includes both                     |
| Mutation annotations        | `mutation_only=true`                                                                                                   |
| Expanded or binary evidence | `expansion="expanded"` or `"binary"`; default `"any"`. See [interaction expansion](../user-guide/expansion_method.md). |
| Same-species interactions   | `intra_species_only=true`                                                                                              |
| Self-interactions           | `self_only=true`; both participants must be the same molecule                                                          |
| Number of records to show   | `max_results` (default `50`)                                                                                           |

**You get:** interaction records with both participants, MIscore, experimental method, interaction type, publication and
IntAct identifier. Multiple records can describe the same pair of partners. Ask explicitly for either unique partners or
individual evidence records.

**Choose your search scope:** the default `match="broad"` searches the accession as free text and can include isoforms
or matches in other fields. Use `match="exact_id"` for a search scoped to the identifier field, particularly when
comparing counts with an advanced search in the IntAct portal. Composite interaction-and-disorder tools use broad scope.

For author searches, use `author`; it matches publication metadata and does not identify first-author papers. A bare
PMID can be supplied as the query through `accession`, but this is a free-text match and can match prefixes. Check the
returned publications before treating the results as belonging to one paper.

For most searches, use the named filters above. Field expressions such as `species:9606` do not work as ordinary
free-text input. If a condition needs advanced syntax, use `advanced_query`, for example
`id:P04637 AND type:"MI:0407"`.

**Check completeness:** `total_elements` describes the server's matching records, while the returned list may be
shorter. For `self_only` or `expansion="binary"`, use `matched` for the filtered count and check `scanned` and
`truncated`: these filters scan up to a limit, and `total_elements` is the count before they are applied.

### `intact_interaction_details`

Use this after finding an interaction to examine its publication and curator annotations.

> For this IntAct interaction, show the publication, experimental host, detection method and curator notes.

**Specify:** the interaction's IntAct identifier (`ebi_id`, beginning with `EBI-`) from the search results.

**You get:** publication details, interaction and detection terms, cross-references and annotations. Use
`intact_interactions` for the participants and `intact_features` for binding regions or mutations.

### `intact_export_interaction`

Use this to obtain an interaction record for analysis in another tool or pipeline.

> Export this interaction in MITAB 2.7 format.

**Specify:** its `ebi_id` and a `format`: `miTab25`, `miTab26`, `miTab27` (default), `miTab28`, `miXML25` or `miXML30`.

**You get:** the record's text content in the requested format. Ask your assistant to save it to a file if your
assistant supports file creation. XML exports can be much larger than a table summary.

## Explore binding regions and mutations

### `intact_features`

Use this to inspect the binding regions, mutations and other curated features associated with one interaction.

> For this interaction, list the annotated binding regions and mutations, their residue ranges, and which participant
> each feature belongs to.

**Specify:** an interaction `ebi_id`. To focus on mutation effects, use `effect_filter`, such as `decreasing`,
`increasing`, `disrupting` or `no effect`.

**You get:** feature types, residue ranges, participant identifiers and mutation effects where annotated. Features may
span several ranges. An empty result can mean either no curated features or an unknown interaction identifier; check
`intact_interaction_details` if needed. At most 200 features are retrieved for one interaction.

### `intact_protein_features`

Use this to collect features across a protein's interactions, rather than inspect each interaction separately.

> Which mutations in human p53 are annotated as disrupting interactions? Show the affected partners, residue ranges
> and IntAct interaction identifiers.

**Specify:** the protein `accession`, optionally `feature_type`, mutation `effect`, `species` and `min_miscore` (default
`0.0`). `max_interactions_to_scan` defaults to `500`.

**You get:** matching features with their partners and interaction identifiers, plus summaries of feature types and
mutation effects. The summaries describe all features in the scanned interactions, before the type or effect filter. If
`truncated` is true, the results cover only the scanned subset, starting with the highest-scoring interactions.

## Explore networks and complexes

### `intact_network`

Use this to explore a protein's immediate interaction neighbourhood or compare the neighbours of two proteins.

> Retrieve the interaction network around human p53 with MIscore at least 0.6. Summarise the nodes and edges and say
> whether the network was truncated.

**Specify:** a protein `accession`, `min_miscore` (default `0.4`) and `max_edges` (default `500`).

**You get:** network nodes and edges, including interaction identifiers, scores and publications. Edges are filtered by
score and capped at the requested limit. Check `truncated` before drawing conclusions about missing connections. To
explore beyond the immediate neighbourhood, request a network for one of the neighbours.

### `intact_complex`

Use this to find complexes containing a protein or inspect a known complex in Complex Portal.

> Find complexes containing human p53, then show the components, stoichiometry and function of one matching complex.

**Specify:** `accession` for a protein or text search, or `complex_ac` for a specific Complex Portal identifier
(`CPX-…`). Search results default to a maximum of 25 (`max_results`).

**You get:** a list of matching complexes, or a complex's composition, function and associated information. Search
results include organism and predicted status. Use the complex identifier from a result to request its full details.

## Get counts and database summaries

### `intact_facets`

Use this to break down a set of interactions without retrieving every evidence record.

> Break down human p53 interactions with MIscore at least 0.6 by detection method.

**Specify:** a free-text `query` (empty for the whole database), a `facet`, and relevant filters such as `species`,
`interaction_type` or `min_miscore` (default `0.0`). Available breakdowns are `species`, `detection_method`,
`interaction_type`, `interactor_type`, `host_organism`, `mutation`, `expansion`, `negative` and `miscore`.

**You get:** counts for each category, or a score histogram for `miscore`. These are counts of interaction records, not
unique partners. Accession searches use broad free-text scope; for identifier-scoped counts of a particular type, use
`intact_interactions` with `match="exact_id"` and `interaction_type`.

### `intact_statistics`

Use this for database-wide totals, coverage and historical trends.

> Summarise IntAct's database coverage, including proteins, interactions and publications. Include the date or source
> of the statistics where available.

**Choose a section:** `summary` (default), `species_coverage`, `detection_methods`, `curation_history`,
`publication_experiment_history` or `interactions_history`.

**You get:** statistics tables. These are periodic snapshots; request `live_count=true` with `section="summary"` if you
also need the live binary-interaction total. Snapshot and live counts can differ. For a filtered search's breakdown, use
`intact_facets`.

## Find protein disorder annotations

DisProt provides curated, experimentally supported annotations. **No DisProt record means no curated evidence was found;
it does not mean the protein is ordered.** Disorder content is reported as a fraction of the sequence: `0.30`
means 30% of residues are annotated as disordered. Treat a percentage cutoff as a selection criterion for your question.

### `disprot_disorder`

Use this to examine disorder annotations for one protein.

> Show the experimentally supported disordered regions of human p53, with residue boundaries, annotation terms and
> evidence methods.

**Specify:** the validated UniProt `accession`.

**You get:** the DisProt identifier, annotated disorder fraction and region-level details. Binding partners and
structural cross-references appear where curated. A missing record is reported explicitly. This tool does not provide
AlphaFold confidence data or a comparison between predicted and experimentally annotated disorder.

### `disprot_search`

Use this to discover proteins by organism, annotation, experimental method, dataset or release.

> Find human DisProt entries annotated with RNA-binding function. Show their identifiers and annotated disorder
> content, and report how many matches were found.

**Specify at least one filter:** `name`, `organism`, `ncbi_taxon_id`, `dataset`, `release`, `acc`, or an ontology
identifier: `idpo_id` for a structural state or transition, `eco_id` for an evidence method, or `go_id` for a function
(for example `GO:0003723` for RNA binding). Filters combine, so results must satisfy all supplied conditions.

**You get:** summary records and the total number of matches (`size`). The displayed list is limited by `max_results`
(default `50`). Follow up with `disprot_disorder` to inspect the region-level evidence for an individual protein.

### `disprot_batch`

Use this to check disorder annotations for a list of proteins, such as a set of interaction partners.

> Check these UniProt accessions in DisProt. Show proteins with at least 30% annotated disorder, and separately list
> those without a DisProt record.

**Specify:** `accessions` (up to 200) and optionally `min_disorder_content`. Duplicate accessions are removed and
isoform suffixes are stripped for the lookup.

**You get:** disorder summaries for matching proteins. `n_found` includes annotated entries below the requested cutoff,
while `entries` contains only those passing it. Missing accessions are listed in `_provenance.missing`; keep these
separate from proteins that have annotations but fall below the threshold.

## Combine interaction and disorder evidence

### `disordered_interactions`

Use this to find interactions where at least one participant meets a chosen DisProt disorder threshold.

> Find human p53 interaction partners with MIscore at least 0.6 where either participant has at least 30% annotated
> disorder. Give one row per partner and make clear whether p53, its partner, or both meet the disorder cutoff.

**Specify:** the protein `accession`, `min_miscore` (default `0.45`), `min_disorder_content` (default `0.30`), and
optionally
`species` or `detection_method`. `max_results` defaults to `50`.

**You get:** one row per unique protein partner by default, with its best-scoring interaction evidence and available
DisProt annotations for both participants. Set `aggregate_by_partner=false` to request individual evidence records.

**Interpret the selection carefully:** the starting protein can satisfy the disorder criterion on its own. A returned
partner is therefore not necessarily annotated as disordered. Non-protein participants are skipped, and isoforms are
combined under their canonical accession for disorder lookup.

Check the numbers of evidence records scanned, partners with disorder data and qualifying partners returned. The default
partner view scans up to 1,000 evidence records (`evidence_scan_limit`); `results_truncated` indicates that the output
limit excluded qualifying partners. Ask the assistant to report both scan limits and output limits.

### `feature_disorder_overlap`

Use this to ask whether IntAct binding regions, mutation sites or other features overlap with DisProt disorder
annotations on the same protein.

> Which annotated binding regions of human p53 overlap with experimentally supported disordered regions? Show the
> feature ranges, overlap lengths, overlap percentages and supporting IntAct identifiers.

**Specify:** the protein `accession`, `min_miscore` (default `0.45`) and `max_interactions_to_scan` (default `50`).

**You get:** features with overlap lengths and fractions, including whether each feature lies entirely within annotated
disorder. Overlapping DisProt disorder annotations are merged so that a residue is counted only once.

The tool scans the highest-scoring interactions up to the requested limit. Features without numeric residue boundaries
cannot be assessed. If no DisProt entry is found, the empty overlap result means there was no annotation to compare. An
overlap locates the feature within annotated disorder; it does not by itself establish a mechanism or causal effect.

### `enrichment_disorder`

Use this to compare disorder among a protein's interaction partners with the curated DisProt set for an organism.

> Test whether human p53's interaction partners with MIscore at least 0.6 are enriched for proteins with at least 30%
> annotated disorder relative to human DisProt entries. Report the assessed partner count, background, enrichment
> ratio and p-value.

**Specify:** the protein `accession`, `min_miscore` (default `0.6`), `min_disorder_content` (default `0.30`) and
`background_taxon_id` (default `9606`, human). Choose the background organism explicitly for non-human analyses.

**You get:** partner and background counts, disorder rates, an enrichment ratio and a hypergeometric p-value. A ratio
above 1 means a higher disorder rate among assessed partners than in the selected background; interpret it alongside the
p-value and sample sizes.

**The background is the curated DisProt set, not the whole proteome.** Its coverage affects what this comparison can
establish. Report how many partners could be assessed and check `partners_truncated`, which flags the interaction scan
limit of 2,000. Large partner sets can take longer to analyse.

## Explore DisProt coverage and releases

### `disprot_statistics`

Use this to summarise annotations for an organism or dataset.

> Summarise annotated disorder content for human entries in DisProt. State how many entries were included and whether
> the statistics cover all matching entries or a sample.

**Specify:** `ncbi_taxon_id`, `organism` or `dataset`. `max_scan` defaults to `2000`.

**You get:** entry and region counts, plus mean, minimum and maximum disorder content. If `sampled=true`, these
statistics describe the scanned sample. They describe DisProt's curated entries, not every protein in that organism.

### `disprot_release_compare`

Use this to see which entries or regions were added or removed between two DisProt releases.

> Compare DisProt releases 2021_12 and 2022_06. Report the numbers of added and removed entries and show a few examples.

**Specify:** `release_a`, `release_b`, and `scope="entries"` or `"regions"` (default). `max_examples` defaults to `20`.

**You get:** counts and examples of additions and removals from the first release to the second. Region comparisons
include all curated region types, not only disorder annotations. This compares entry or region identifiers; it is not a
full account of every annotation edit. Comparing two releases may take longer than an individual protein lookup.

### `disprot_list_ids`

Use this when you need a list of DisProt identifiers as the starting point for further lookups.

> List 20 DisProt identifiers.

**Specify:** an optional `limit`.

**You get:** identifiers such as `DP00003`, with total and returned counts. For proteins matching a biological question,
use `disprot_search` instead.

## Check the connection

### `ping`

Use this if you want to confirm that your assistant can reach IntAct–MCP.

> Check whether the IntAct–MCP server is reachable.

No input is required. A successful response identifies the server and its version. If it fails, check that the connector
is enabled and that its URL matches the [connection guide](../user-guide/mcp.md).

## Read the answer with its scope in mind

Before using a result in a table, figure or analysis, ask your assistant to include:

- **Identifiers and evidence:** protein accessions, IntAct interaction identifiers, DisProt identifiers and publications
  where available.
- **Selection criteria:** organism, MIscore cutoff, disorder threshold and any method or interaction-type filters.
- **What was counted:** unique partners, interaction evidence records, annotated regions or database entries.
- **Completeness:** total matches, returned results, scan limits and any truncation or sampling indicators.
- **Missing annotations:** distinguish absent curated evidence from evidence that a feature or interaction is absent.

For comparisons across tools, set thresholds explicitly: their defaults differ. If a result is empty, check the protein
identity, organism and filters before interpreting it biologically.
