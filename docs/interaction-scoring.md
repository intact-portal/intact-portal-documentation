# Interaction Scoring

## MIscore

MIscore is a customizable, heuristic scoring system that takes three factors into account:

1. How the interaction was observed, predicted or inferred \(interaction detection method; MI:0001\)
2. The type of interaction. Direct interaction, physical association, co-localization and so forth. \(interaction type; MI:0190\)
3. The number of publications reporting a specific interaction

MIscore provides a score that represents the degree of confidence in the existence of a particular interaction by assessing the annotation of that specific interaction in a standards-compliant dataset. The score given to an interaction will increase as the number of experimental evidences supporting that interaction increases. Experimental evidences contribute more highly to the final score than evidences derived by predictive algorithms or literature text-mining methods. Combinations of evidences, such as low scoring experimental interactions \(e.g. co-localizations\) supported by non-experimental evidence provide a higher degree of confidence than either would in isolation. In the versions of MIscore implemented by the IntAct database and for the filtering of data for export from IntAct to UniProtKB, the values have been selected to reflect the ethos of these databases, with a strong emphasis on there being experimental evidence for the existence of a physical interaction.

![](../.gitbook/assets/image%20%284%29.png)

## Score calculation

By default MIscore presents a normalized score \(_S_MI\) between 0 and 1 reflecting the reliability of its combined experimental evidence. This score is calculated from the weighted sum of the three different sub-scores listed above: number of publications \(_p_\), experimental detection methods \(_m_\) and interaction types \(_t_\) found for the interaction. The importance of each variable in the main equation can be adjusted using a weight factor. Each of these sub-scores is also represented by a score between 0 and 1.

![](../.gitbook/assets/image%20%281%29.png)

The MIscore normalized score calculates a composite score for an interaction based on the number of publications reporting the interaction, the reported interaction detection methods and interaction types.

### Publication score

The publication score takes into account the number of different publications supporting an interaction.

![](../.gitbook/assets/image%20%282%29.png)

_n_![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)![\[equivalent\]](https://europepmc.org/corehtml/pmc/pmcents/equiv.gif)![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)Number of publications reporting the interaction \|\| Sp ≡n ∈N \[0,1,2,3 ...\].

_b_![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)![\[equivalent\]](https://europepmc.org/corehtml/pmc/pmcents/equiv.gif)![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)Number of publications with maximum score; default: b![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)7

### Method score

The method score takes into account the diversity of interaction detection methods reported for an interaction.

![](../.gitbook/assets/image%20%286%29.png)

_scv_ is a normalized score between 0 and 1 associated to an interaction detection method term, as defined by the MI ontology. An MI detection method ontology term without an assigned score inherits the score from the nearest parent. _Gscv_ represents a category of scores normally grouping scores with a common parent. _n_ is the number of times an ontology term is reported. The _scv_ score values are customizable; however, detection method ontology terms are assigned with a default score based on the assessment of the HUPO PSI–MI consortium:

scv1![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)1.00 \|\| cv1![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0013 \| biophysical

scv2![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.66 \|\| cv2![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0090 \| protein complementation assay

scv3![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.10 \|\| cv3![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0254 \| genetic interference

scv4![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.10 \|\| cv4![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0255 \| post![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)transcriptional interference

scv5![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)1.00 \|\| cv5![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0401 \| biochemical

scv6![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.33 \|\| cv6![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0428 \| imaging technique

scv7![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.05 \|\| cv7![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)unknown \| unknown

Gscv1![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)scv1 \| Gscv2![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)scv2 \| Gscv3![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)scv3 \| Gscv4![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)scv4\|Gscv5![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)scv5 \| Gscv6![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)scv6

### Type score

The interaction type score takes into account the diversity of interaction types reported for an interaction.

_St_![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)![\[equivalent\]](https://europepmc.org/corehtml/pmc/pmcents/equiv.gif)![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)Type Score \|![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)\| St![\[set membership\]](https://europepmc.org/corehtml/pmc/pmcents/x2208.gif) \[0−1\]

_St_\(_cvi_\)![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)log\(_b_![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)+![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)1\)\(_a_![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)+![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)1\)

_a_![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)∑\(_scvi_![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)×![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)_ni_\)

_b_![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)_a_![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)+![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)∑\(_Max_\(_Gscvi_\)\)

As in the method score, _scv_ is a normalized score between 0 and 1, in this case associated to an interaction type CV term. An MI-type ontology term without an assigned score inherits the score from the nearest parent. Interaction-type scores are also customizable but by default they have assigned a heuristic score based on the assessment of the HUPO PSI–MI consortium:

scv1![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.10 \|\| cv1![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0208 \| genetic interaction

scv2![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.33 \|\| cv2![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0403 \| colocalization

scv3![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.33 \|\| cv3![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0914 \| association

scv4![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.66 \|\| cv4![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0915 \| physical association

scv5![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)1.00 \|\| cv5![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)MI:0407 \| direct interaction

scv6![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)0.05 \|\| cv6![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)unknown \| unknown

Gscv1![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)scv1 \| Gscv2![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)scv2 \| Gscv3![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)=![ ](https://europepmc.org/corehtml/pmc/pmcents/x2009.gif)scv3, scv4, scv5

More details including examples of how to use MIscore are available at [https://europepmc.org/articles/PMC4316181/](https://europepmc.org/articles/PMC4316181/) and [https://code.google.com/p/miscore/](https://code.google.com/p/miscore/).

