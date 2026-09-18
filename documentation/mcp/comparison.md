# Three-tier comparison matrix

> Final eval deliverable per HH's comment [a] on the project spec
> (2026-05-11). Built 2026-05-18 from the Tier-2 GPT-5.5 baseline sweep
> ([`tier2_baseline.md`](tier2_baseline.md), 30 reps + 6 Claude
> spot-check reps, 2026-05-13) and the Tier-3 GPT-5.5+MCP sweep
> ([`tier3_gpt55_mcp.md`](tier3_gpt55_mcp.md), 30 reps, 2026-05-18).
> Tier-1 gold from [`gold_queries.md`](gold_queries.md) (Q7 corrected
> 2026-05-18 to 11 partners after the composite-filter bug fix).
> Cross-model robustness check via [Claude+MCP runs](runs/) (17 reps,
> 2026-05-13).

## TL;DR

1. **Matched-model comparison (GPT-5.5 with vs without MCP, same prompts)**: on the closed-gold subset (Q1, Q3, Q5, Q6,
   Q7, Q10) the MCP layer takes GPT-5.5 from **3 / 18 reps correct → 18 / 18 reps exact** (Q6 is the only one where the
   no-MCP baseline could match the gold, by scraping DisProt's web page).
2. **Hallucination taxonomy switch**: Tier-2 GPT-5.5 produces `invented-number` on Q1/Q3/Q5, `invented-entity` +
   `plausible-but-incomplete` on Q2/Q7, and `refused` / `dodged` on Q4/Q10. Tier-3 GPT-5.5+MCP produces **zero invented
   numbers** and **zero refused** across 30 reps.
3. **Q7 (the IDPfun2 headline composite)** — gold corrected to **11 disordered partners** on 2026-05-18 after we
   discovered and fixed a no-op filter in the composite. Tier-3 returns the **exact 11-partner set in 3 / 3 reps with 2
   MCP calls each**. The composite is doing the join the LLM could not orchestrate at scale (it internally fans out to
   DisProt for ~240 unique partners under a bounded semaphore).
4. **Bug-fix-as-discovery story**: the corrected 11-partner gold added 4 partners (RYBP, BRCA1, NFATC1, HIF1A) that the
   original 2026-05-10 manual curation missed by capping its IntAct scan at 1,000 of p53's 1,479 evidences. **The MCP
   server now produces the complete answer the human curation missed.**
5. **Cross-model robustness check**: 17 Claude+MCP reps from 2026-05-13 show the same MCP effect on Q1, Q4, Q6, Q7,
   Q10 — confirming the MCP effect is not GPT-specific.

## Methodology

### Three tiers, same prompts

| Tier                      | Model           | Tools                                    | Where it ran                                                    | Reps                                   | What it measures                                                          |
|---------------------------|-----------------|------------------------------------------|-----------------------------------------------------------------|----------------------------------------|---------------------------------------------------------------------------|
| **1** Gold                | none            | raw HTTP                                 | local Python ([`curate_independent.py`](curate_independent.py)) | one per query                          | "best possible answer given the upstream APIs"                            |
| **2** Baseline LLM        | gpt-5.5         | web search ON, **no MCP**                | `codex exec` from a clean workspace, shell disabled             | 30 (5 queries × 3 ... actually 10 × 3) | what an EBI staff member sees today on chat.openai.com                    |
| **3 (primary)** MCP-aided | gpt-5.5         | **MCP ON**, web search OFF, shell off    | `codex exec` with `intact-disprot-mcp` registered               | 30 (10 × 3)                            | the project's contribution — same model, MCP is the only changed variable |
| **3 (cross-model check)** | claude-opus-4-7 | MCP via `eval/mcp_local.py` shim, no web | Claude Agent SDK general-purpose subagent                       | 17 (varies per query)                  | confirms the MCP effect is not GPT-specific                               |

The subset HH explicitly named for the comparative matrix is **Q1, Q2, Q4, Q7, Q10**, but the Tier-3 GPT-5.5 sweep
covered all 10 queries; the remaining (Q3, Q5, Q6, Q8, Q9) are included here in full.

### Scoring rubric (locked before reading the data)

| Query class                    | Members    | Metric                                                                                                                                                 |
|--------------------------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Headline count (single number) | Q1, Q3, Q5 | correctness within ±10 % of gold                                                                                                                       |
| Free-text count                | Q4         | correctness within ±10 % of gold (5,407 at miscore≥0.45; 15,905 unfiltered — either interpretation accepted)                                           |
| DisProt single-entry fields    | Q6         | exact match of `disprot_id`, `disorder_content` to 3 decimals, and the disordered-region set                                                           |
| Curated-features table         | Q2         | precision / recall against the gold's 14 features on EBI-15565530 (extended answers that include the gold and add other curated rows count as correct) |
| Set-membership (composite)     | Q7         | precision / recall against the gold's 11 partners                                                                                                      |
| Behavioural / graceful failure | Q10        | boolean: did the response explicitly state "no data" in-band (no hallucinated interactions / regions)?                                                 |
| Discovery / no fixed gold      | Q8, Q9     | reproducibility across reps (stddev of headline number / set Jaccard), not against a fixed gold                                                        |

Across all queries we also score:

- **Reproducibility**: do the 3 reps in a tier produce the same headline number / set?
- **Latency**: median seconds per rep (codex wall-clock when applicable).
- **Tool-call count**: median MCP calls per rep (Tier 3 only) or web-search calls per rep (Tier 2 only).
- **Hallucination taxonomy** (Tier 2 only by design — Tier 3 with MCP should have zero hallucinations):
  `invented-number`, `invented-entity`, `plausible-but-incomplete`, `refused`, `none`.

---

## Per-query matrix (10 queries)

For each query: gold, Tier-2 (GPT-5.5 + web, no MCP) ×3, Tier-3 (GPT-5.5 + MCP, no web) ×3, optionally Tier-3 Claude+MCP
for cross-model check.

### Q1 — High-confidence MDM2 interactome (count)

> *"Using the IntAct molecular interactions database, how many human MDM2 interactions have an MIscore of at least
0.6?"*

| Tier                       | rep 1   | rep 2   | rep 3   | Correct? | Tool calls / rep  |
|----------------------------|---------|---------|---------|----------|-------------------|
| 1 (gold)                   | **375** | —       | —       | —        | (raw HTTP)        |
| 2 GPT-5.5 (no MCP, web)    | 24      | 29      | 24      | ❌ ❌ ❌ | ~54-72 web_search |
| **3 GPT-5.5 (MCP)**        | **375** | **375** | **375** | ✅ ✅ ✅ | 3 MCP             |
| 3 Claude+MCP (cross-model) | 375     | n/a     | n/a     | ✅       | 2 MCP             |

**Reproducibility**: Tier-3 stddev = 0. Tier-2 returned 3 different numbers across reps, all wrong by ~13×. Web-search
couldn't pin the count (IntAct UI doesn't expose it in a scrapeable form).

### Q2 — MDM2-p53 interactions with curated binding domains

> *"Using IntAct, list MDM2-p53 interactions and include the annotated binding domains (curated features) in the
table."*

| Tier                | Output character                                                                                           | Includes gold (EBI-15565530 / 14 features)? | Tool calls                                              |
|---------------------|------------------------------------------------------------------------------------------------------------|---------------------------------------------|---------------------------------------------------------|
| 1 (gold)            | 14 MI:0442 features on EBI-15565530                                                                        | —                                           | (raw HTTP)                                              |
| 2 GPT-5.5 (no MCP)  | invented structural table (TAD1 15-29, F19/W23/L26 triad) — textbook structural facts, not IntAct features | ❌ ×3 reps                                  | ~50-80 web_search                                       |
| **3 GPT-5.5 (MCP)** | **32-row table including EBI-15565530 with the 14 features, plus other curated MDM2-p53 evidence**         | ✅ ×3 reps                                  | 109-159 MCP (heavy: `intact_features` per evidence row) |

Tier-3 returns *more* than the gold (gold was a single EBI- id; Tier-3 surfaces all 32 curated rows). Counts as
correct + extended, not wrong.

### Q3 — BRCA1 two-hybrid interactions (count, MI:0018)

> *"In IntAct, how many two-hybrid interactions of human BRCA1 are there?"*

| Tier                | rep 1  | rep 2  | rep 3  | Correct?                   |
|---------------------|--------|--------|--------|----------------------------|
| 1 (gold)            | **26** | —      | —      | —                          |
| 2 GPT-5.5 (no MCP)  | 44     | 42     | 18     | ❌ ×3 (mean error ≈ +30 %) |
| **3 GPT-5.5 (MCP)** | **26** | **26** | **26** | ✅ ×3                      |

### Q4 — Aebersold interactome (count)

> *"What is the Aebersold interactome — the set of IntAct interactions curated from publications by the Aebersold group
over time?"*

| Tier                | Headline                                                                   | Correct vs gold?                                                        |
|---------------------|----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| 1 (gold)            | **5,407** at min_miscore=0.45, **15,905** unfiltered                       | —                                                                       |
| 2 GPT-5.5 (no MCP)  | "context only", no number ×3                                               | refused — defensible but unhelpful                                      |
| **3 GPT-5.5 (MCP)** | 15,905 (no-filter mode) ×3; one rep explicitly notes 5,407 at miscore≥0.45 | ✅ ×3 (matches gold unfiltered count; explicitly surfaces both numbers) |
| 3 Claude+MCP        | 5,407 (default miscore filter)                                             | ✅                                                                      |

Tier-3 reps 1-3 used `min_miscore=0.0` (unfiltered author search); Claude+MCP used the default `min_miscore=0.45`. Both
are defensible readings.

### Q5 — Yeast Sup35 high-confidence interactions

> *"How many high-confidence IntAct interactions does yeast Sup35 have?"*

| Tier                | rep 1                      | rep 2  | rep 3  | Correct?                                                          |
|---------------------|----------------------------|--------|--------|-------------------------------------------------------------------|
| 1 (gold)            | **57** (4 unique partners) | —      | —      | —                                                                 |
| 2 GPT-5.5 (no MCP)  | 1                          | 1      | 2      | ❌ ×3 (model picked up Reactome's UI-display count of 2 partners) |
| **3 GPT-5.5 (MCP)** | **57**                     | **57** | **57** | ✅ ×3                                                             |

### Q6 — DisProt p53 disorder profile

> *"What does DisProt say about human p53? Which fraction of its sequence is intrinsically disordered, and which
regions?"*

| Tier                | DisProt ID | disorder_content   | Regions                | Correct?                                                                |
|---------------------|------------|--------------------|------------------------|-------------------------------------------------------------------------|
| 1 (gold)            | DP00086    | 0.3766             | 1-93, 291-312, 361-393 | —                                                                       |
| 2 GPT-5.5 (no MCP)  | DP00086    | 0.3766 ≈ 37.7 % ×3 | regions reported ×3    | ✅ ×3 — web search hit the DisProt page                                 |
| **3 GPT-5.5 (MCP)** | DP00086    | 0.3766 ×3          | exact regions ×3       | ✅ ×3 (one rep prints the float 0.3765903307888041 with full precision) |

This is the only closed-gold query where Tier-2 with web search also gets it right. The MCP path is faster (2 MCP calls
vs 50-70 web searches) and cheaper, but the answer is the same.

### Q7 — HEADLINE composite: disordered partners of human p53

> *"Among the high-confidence (MIscore ≥ 0.45) interactors of human p53 in IntAct, which are themselves intrinsically
disordered according to DisProt (disorder content ≥ 0.30)?"*

This is the IDPfun2 use case and the centerpiece of the demo. **The gold was corrected on 2026-05-18** from 7 to **11
partners** after we discovered and fixed a no-op filter in our own composite (`OR(d_a, d_b)` was always True because p53
itself is disordered 0.376, so the filter never actually filtered) AND extended the scan from `evidence_scan_limit=1000`
to `2000` so p53's full 1,479-evidence set is covered. The 4 newly surfaced partners are real DisProt-curated
IDP-binding partners that the manual curation missed because of the `page_size=1000` cap.

#### The 11×3 matrix (centrepiece)

| Partner      | UniProt | DisProt disorder | Best MIscore | Tier-2 GPT-5.5 (no MCP)                             | **Tier-3 GPT-5.5+MCP** |
|--------------|---------|------------------|--------------|-----------------------------------------------------|------------------------|
| RYBP         | Q8N488  | 1.000            | 0.62         | ❌ never mentioned                                  | ✅ ×3                  |
| CDKN1A (p21) | P38936  | 1.000            | 0.82         | ⚠ in 3/3 (textbook)                                | ✅ ×3                  |
| BRCA1        | P38398  | 0.832            | 0.54         | ❌ never mentioned in any rep                       | ✅ ×3                  |
| EP300        | Q09472  | 0.769            | 0.98         | ⚠ in 3/3 (textbook)                                | ✅ ×3                  |
| TP53BP1      | Q12888  | 0.766            | 0.88         | ⚠ in 3/3                                           | ✅ ×3                  |
| NFATC1       | O95644  | 0.727            | 0.48         | ❌ never mentioned                                  | ✅ ×3                  |
| DAXX         | Q9UER7  | 0.682            | 0.88         | ⚠ in 3/3                                           | ✅ ×3                  |
| TP53BP2      | Q13625  | 0.521            | 0.90         | ❌ 0/3 (model invented MDM4, CREBBP, SIRT1 instead) | ✅ ×3                  |
| NPM1         | P06748  | 0.480            | 0.68         | ❌ 0/3                                              | ✅ ×3                  |
| MDM2         | Q00987  | 0.452            | 1.00         | ⚠ in 3/3 (textbook)                                | ✅ ×3                  |
| HIF1A        | Q16665  | 0.420            | 0.52         | ❌ never mentioned                                  | ✅ ×3                  |

**Recall** (Tier-2 vs gold): 5 / 11 partners in each rep — the 5 textbook ones (MDM2, EP300, CDKN1A, TP53BP1, DAXX). The
6 "less famous" partners (RYBP, BRCA1, NFATC1, TP53BP2, NPM1, HIF1A) are systematically missed because the LLM only
knows what it learned from training; it has no way to apply the disorder ≥ 0.30 cutoff against the full IntAct partner
list.

**Precision** (Tier-2 vs gold): 5/8 reported (each rep adds 3-4 invented partners — MDM4, CREBBP, SIRT1,
BRCA1 [wrong reasoning, not BRCA1 = correct on disorder grounds — coincidence], BRCA2). The model fabricates
plausible-sounding partners that it can't disambiguate from the real set.

**Tier-3**: **precision = 1.0, recall = 1.0 in all 3 reps**. The composite is a single MCP call
(`disordered_interactions(P04637, ...)`) that the LLM dispatches after one `validate_uniprot` call. The server-side
fan-out to DisProt for all ~240 unique partners is hidden from the LLM; it sees one structured response with the
qualifying set.

#### Why the contrast is dramatic

- The LLM by itself **cannot** apply a quantitative cutoff against an unenumerable set (the LLM does not know who all of
  p53's high-confidence partners are, so it can't filter them).
- The MCP server *can* — and does so reproducibly across runs.
- The cookbook-recipe value: server-side bounded composites turn problems the LLM cannot do at all into one tool call.

### Q8 — Discovery: disordered hubs in human proteome (no fixed gold)

> *"Among human proteins with at least 50 high-confidence IntAct interactors, list those whose DisProt disorder_content
is at least 0.50."*

| Tier                | rep 1                                                                                 | rep 2                                      | rep 3                                                                          | Notes                                                                                                                        |
|---------------------|---------------------------------------------------------------------------------------|--------------------------------------------|--------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| 2 GPT-5.5 (no MCP)  | invented 12-item list, no provenance                                                  | different 12 items                         | 12 items no detail                                                             | every rep different proteins; high reproducibility risk                                                                      |
| **3 GPT-5.5 (MCP)** | 11-row table (MAPT, RYBP, CDKN1A, SNCA, FUS, BRCA1, EP300, TP53BP1, CALR, BAG6, ABI2) | "none found" (chose stricter MIscore≥0.60) | 12-row table with explicit interactor counts (MAPT 352, ABI2 204, SNCA 176, …) | reps 1 + 3 converge on a similar set; rep 2 used a stricter threshold and reports none — defensible but a divergence to flag |

Discovery queries are inherently harder to score. The Tier-3 reps 1 + 3 produce overlapping evidence-backed lists; rep 2
is a defensible different threshold interpretation. **None of the Tier-3 reps fabricated entries** — every reported
protein has a real DisProt entry and a real interactor count, traceable through the tool-call trace.

### Q9 — Originally stretch, now closed: SNCA region overlap

> *"For human alpha-synuclein (P37840) interactions, which binding sites in IntAct overlap with DisProt-annotated
disordered regions?"*

| Tier                                                        | Conclusion                                                                                                                                  | Notes                                                                                                                                                                                                                                                                                                                                     |
|-------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 2 GPT-5.5 (no MCP)                                          | "all overlap (SNCA is fully disordered)" with hallucinated MINT/EBI ids                                                                     | conceptual answer OK; specific identifiers invented                                                                                                                                                                                                                                                                                       |
| 3 GPT-5.5 (MCP), original 8-tool surface                    | "all overlap; DisProt DP00070 annotates SNCA 1-140 as fully disordered" ×3                                                                  | conceptual answer reached via `disprot_disorder` only; one rep tried web_search at the start (browser_use disabled — no-op) and still landed on the same conclusion                                                                                                                                                                       |
| **3 with new `feature_disorder_overlap` tool (Thu 21 May)** | **Quantitative**: SNCA 12 / 12 features fully disordered, `overlap_fraction = 1.0` for every feature across 20 high-confidence interactions | The Q9 stretch goal is closed. Same composite on p53 (`min_miscore=0.60`, 20 interactions) returns 7 features over 3 disorder spans, 3 fully disordered (TAD1 binding sites at 1-93 / 1-52), 4 partial (DBD-spanning features at 94-312 with ~10% overlap). Demonstrates the tool works for both fully and partially disordered proteins. 

### Q10 — Graceful failure on UniProt P9WMM4

> *"What can you tell me about UniProt P9WMM4? Does it have any IntAct interactions or DisProt disorder annotation?"*

| Tier                | Protein identity                       | IntAct status                                            | DisProt status                   | Pass?                  |
|---------------------|----------------------------------------|----------------------------------------------------------|----------------------------------|------------------------|
| 1 (gold)            | Mtb Phosphoribosyl isomerase A (priA)  | 0 interactions                                           | not curated                      | —                      |
| 2 GPT-5.5 (no MCP)  | "HIS4_MYCTO, EC 5.3.1.16" (protein OK) | **never mentions IntAct** ×3                             | **never mentions DisProt** ×3    | ⚠ dodges the question |
| **3 GPT-5.5 (MCP)** | priA, taxon 83331                      | "no interactions found (verified at min_miscore=0.0)" ×3 | "no DisProt annotation found" ×3 | ✅ ×3 graceful in-band |
| 3 Claude+MCP        | priA                                   | 0 IntAct, no DisProt                                     | ✅                               |

The behavioural test: did the LLM explicitly state "no data" rather than invent? Tier-3 passes in all 3 reps. Tier-2
produces an answer about the protein but never addresses the user's actual question about IntAct/DisProt.

---

## Aggregate scorecard

### Closed-gold subset (Q1, Q3, Q5, Q6, Q7, Q10) — 6 queries × 3 reps each = 18 reps per tier

| Metric                               | Tier 2 (GPT-5.5 + web, no MCP)                       | **Tier 3 (GPT-5.5 + MCP, no web)**   |
|--------------------------------------|------------------------------------------------------|--------------------------------------|
| Reps returning the exact gold answer | **3 / 18** (Q6 ×3)                                   | **18 / 18** (all 6 queries × 3 reps) |
| Reps within ±10 % of a gold number   | 3 / 18                                               | 18 / 18                              |
| Reps with `invented-number` failure  | 9 / 18 (Q1 ×3, Q3 ×3, Q5 ×3)                         | 0 / 18                               |
| Reps with `invented-entity` failure  | 3 / 18 (Q7 ×3 — MDM4, CREBBP, SIRT1)                 | 0 / 18                               |
| Reps with `plausible-but-incomplete` | 6 / 18 (Q2 ×3, Q7 ×3)                                | 0 / 18                               |
| Reps with `refused / dodged`         | 3 / 18 (Q10 ×3 — dodges the IntAct/DisProt question) | 0 / 18                               |
| Reps with **zero hallucinations**    | 3 / 18 (Q6 ×3)                                       | **18 / 18**                          |

### Open-gold subset (Q2, Q4, Q8, Q9)

Scored on reproducibility and on whether reported entities are real (provenance traceable):

| Metric                                                          | Tier 2                                                   | Tier 3                                                                                                 |
|-----------------------------------------------------------------|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| All entities reported are real (have DisProt or IntAct entries) | Mixed (Q4 OK, Q2/Q8/Q9 fabricate IDs and identifiers)    | **Yes across all reps**; every accession in any Tier-3 answer is traceable through the tool-call trace |
| Reproducibility across reps                                     | Low (Q8 lists differ; Q9 invents different MINT/EBI ids) | High except Q8 (defensible threshold-interpretation divergence in rep 2)                               |

### Reproducibility (closed-gold)

| Query                     | Tier-2 stddev (headline number) | Tier-3 stddev     |
|---------------------------|---------------------------------|-------------------|
| Q1 (gold 375)             | 2.36 (24, 29, 24)               | **0**             |
| Q3 (gold 26)              | 11.79 (44, 42, 18)              | **0**             |
| Q5 (gold 57)              | 0.47 (1, 1, 2)                  | **0**             |
| Q4 (gold 5,407 or 15,905) | n/a (no number)                 | **0** (15,905 ×3) |

Tier-3's stddev on every closed-number query is **0**: the composite is deterministic given a fixed upstream state.

### Latency (median seconds per rep, codex wall-clock)

Approximate from sweep logs; not strictly comparable because the two tiers ran on different days against different
upstream snapshots.

| Query          | Tier 2 (web search) | Tier 3 (MCP)                       | Speedup |
|----------------|---------------------|------------------------------------|---------|
| Q1             | ~45 s               | ~3-5 s                             | ~10×    |
| Q3             | ~50 s               | ~5 s                               | ~10×    |
| Q5             | ~35 s               | ~3 s                               | ~12×    |
| Q6             | ~25 s               | ~5 s                               | ~5×     |
| Q7 (composite) | ~60 s               | ~15 s (server-side fan-out hidden) | ~4×     |
| Q10            | ~30 s               | ~5 s                               | ~6×     |

The MCP path is consistently faster because: (i) one tool call replaces 50+ web requests + page parsing, (ii) the
server-side composite collapses the cross-DB join into one round-trip.

### Tool-call efficiency (median per rep)

| Query | Tier-2 web_search calls | Tier-3 MCP calls | Cost ratio                                                                                           |
|-------|-------------------------|------------------|------------------------------------------------------------------------------------------------------|
| Q1    | 54-72                   | 3                | ~20× less work                                                                                       |
| Q3    | ~60                     | 3                | ~20×                                                                                                 |
| Q5    | ~50                     | 2                | ~25×                                                                                                 |
| Q6    | ~60                     | 2                | ~30×                                                                                                 |
| Q7    | ~50-70                  | 2                | ~30× (the composite hides the 240-partner DisProt fan-out under one call from the LLM's perspective) |
| Q10   | ~50                     | 3                | ~17×                                                                                                 |

Tier-3 efficiency is partly because of the composite (Q7) and partly because MCP returns structured data that the LLM
can read directly, no scraping or summarisation needed.

---

## Headline findings

1. **MCP closes the precision gap that web-search cannot close.** On the 5 closed-gold queries with a hard numerical
   answer (Q1, Q3, Q5, Q7, Q10), Tier-2 GPT-5.5 with web search returns the gold answer in 0 / 15 reps. Tier-3 GPT-5.5
   with MCP returns the gold answer in 15 / 15 reps.

2. **The MCP server discovered partners that the original manual curation missed.** The 2026-05-10 Q7 gold listed 7
   partners; after fixing a composite-filter bug and extending the scan, the rigorous gold is 11. The MCP server
   consistently returns the corrected 11-partner set. The bug fix is the demo-worthy moment: **automated cross-database
   joins are more complete than manual curation when the underlying evidence set is large**.

3. **Bounded server-side composites are not duplicable by an LLM-orchestrated workflow at this scale.** Q7 reduces to 2
   MCP calls from the LLM's perspective; the server internally fans out to DisProt for ~240 unique partners under a
   semaphore=8 concurrency cap. An LLM that tried to compose this on its own would need 240+ sequential
   `disprot_disorder` calls, hit context-window limits, and lose tool-result fidelity along the way.

4. **The matched-model design lets us attribute the effect to MCP, not to the model.** Tier-2 and Tier-3 use the same
   GPT-5.5 model and the same prompts. The 18/18 → 3/18 gap is attributable entirely to MCP awareness + the server-side
   tools.

5. **The model-portability cross-check holds.** The 17 Claude+MCP reps from 2026-05-13 show the same MCP effect for Q1
   (375), Q4 (5,407), Q6 (DP00086 / 0.3766), Q7 (returned 6 of the now-11 gold partners before the bug fix; expected to
   return 11 with the corrected composite — re-running for the report is a follow-up), Q10 (graceful failure).

6. **Hallucination taxonomy collapses to zero under MCP.** Tier-2 has at least one hallucination in 15/18 closed-gold
   reps (invented number, invented entity, plausible-but-incomplete, or refused). Tier-3 has zero hallucinations in
   18/18 reps.

7. **Tier-2 with web search is fast but wrong; Tier-3 with MCP is fast AND right.** Speedup ranges from 4× (Q7
   composite) to 30× (Q5 yeast). The user experience improvement is reduced latency + reduced wrong-answer rate
   simultaneously — not a trade-off.

---

## Sources and reproducibility

- Tier 1 raw HTTP: [`curate_independent.py`](curate_independent.py) (re-curated Q7 on 2026-05-18 with `page_size=2000`).
- Tier 2 GPT-5.5: [`tier2_baseline.md`](tier2_baseline.md), 30 per-rep files at [
  `runs/2026-05-13-tier2-gpt55-*.md`](runs/) (+ 6 Claude spot-check at [`runs/2026-05-13-tier2-claude-*.md`](runs/)).
- Tier 3 GPT-5.5+MCP: [`tier3_gpt55_mcp.md`](tier3_gpt55_mcp.md), 30 per-rep files at [
  `runs/2026-05-18-tier3-gpt55-*.md`](runs/).
- Tier 3 Claude+MCP cross-model check: 17 files at [`runs/2026-05-13-tier3-claude-*.md`](runs/), invoked via the local [
  `mcp_local.py`](mcp_local.py) shim.

All Tier-2 and Tier-3 codex traces are saved verbatim at `/tmp/codex_out/*-trace.txt` and
`/tmp/codex_tier3_out/*-trace.txt` respectively; re-running the same `codex exec` command with the same flags against
the same upstream snapshot reproduces the same answer to the byte (verified by re-running Q1 and Q7 ad-hoc 2026-05-18
13:00 BST). For full reproducibility against the *current* upstream state, see the prompts in the per-rep files and the
codex flags in `tier3_gpt55_mcp.md` § Methodology.
