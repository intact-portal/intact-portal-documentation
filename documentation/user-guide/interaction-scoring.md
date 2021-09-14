# Interaction Scoring

## MIscore

MIscore is a customizable, heuristic scoring system that takes three factors into account:

1. How the interaction was observed, predicted or inferred \(interaction detection method; MI:0001\)
2. The type of interaction. Direct interaction, physical association, co-localization and so forth. \(interaction type; MI:0190\)
3. The number of publications reporting a specific interaction

MIscore provides a score that represents the degree of confidence in the existence of a particular interaction by assessing the annotation of that specific interaction in a standards-compliant dataset. The score given to an interaction will increase as the number of experimental evidences supporting that interaction increases. Experimental evidences contribute more highly to the final score than evidences derived by predictive algorithms or literature text-mining methods. Combinations of evidences, such as low scoring experimental interactions \(e.g. co-localizations\) supported by non-experimental evidence provide a higher degree of confidence than either would in isolation. In the versions of MIscore implemented by the IntAct database and for the filtering of data for export from IntAct to UniProtKB, the values have been selected to reflect the ethos of these databases, with a strong emphasis on there being experimental evidence for the existence of a physical interaction.

![MI Score Sources](../.gitbook/assets/MIScore.png)

## Score calculation

By default MIscore presents a normalized score \($S\_{\text{MI}}$\) between 0 and 1 reflecting the reliability of its combined experimental evidence. This score is calculated from the weighted sum of the three different sub-scores listed above: number of publications \($p$\), experimental detection methods \($m$\) and interaction types \($t$\) found for the interaction. The importance of each variable in the main equation can be adjusted using a weight factor. Each of these sub-scores is also represented by a score between 0 and 1.

$$
\begin{aligned}
    S_{\text{MI}} &= \frac{K_p \cdot S_p(n) + K_m \cdot S_m(cv) + K_t \cdot S_t(cv)}{K_p + K_m + K_t}\\
    K_{[p,m,t]} &\equiv \text{Weight factor} \in [0,1]\\
    S_{[p,m,t]} &\equiv \text{Scores} \in [0,1]\\
\end{aligned}
$$

The MIscore normalized score calculates a composite score for an interaction based on the number of publications reporting the interaction, the reported interaction detection methods and interaction types.

### Publication score

The publication score takes into account the number of different publications supporting an interaction.

$$
\begin{aligned}
    S_p &\equiv \text{Publication Score} \in [0,1]\\
    S_p &= \log _{(b+1)} (n+1)\\
    n \in \N &\equiv \text{Number of publications reporting the interaction} \\
    b \in \N &\equiv \text{Number of publications with maximum score; default} \; b  =  7
\end{aligned}
$$

### Method score

The method score takes into account the diversity of interaction detection methods reported for an interaction.

$$
\begin{aligned}
    S_m &\equiv \text{Method Score} \in [0,1]\\
    S_m (\text{cv}_i) &= \log _{(b+1)}(a+1)\\
    a &= \sum(scv_i \times n_i)\\
    b &= a + \sum(\max(Gscv_i))
\end{aligned}
$$

$scv\_i$ is a normalized score between 0 and 1 associated to an interaction detection method term, as defined by the MI ontology. An MI detection method ontology term without an assigned score inherits the score from the nearest parent. $Gscv\_i$ represents a category of scores normally grouping scores with a common parent. $n$ is the number of times an ontology term is reported. The $scv\_i$ score values are customizable; however, detection method ontology terms are assigned with a default score based on the assessment of the HUPO PSI–MI consortium:

| $cv\_i$ | $cv\_1$ | $cv\_2$ | $cv\_3$ | $cv\_4$ | $cv\_5$ | $cv\_6$ | $cv\_7$ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Name | biophysical | protein complementation assay | genetic interference | post transcriptional interference | biochemical | imaging technique | Unkwown |
| MI Id | MI:0013 | MI:0090 | MI:0254 | MI:0255 | MI:0401 | MI:0428 | Unkwown |
| $scv\_i$ | $1.00$ | $0.66$ | $0.10$ | $0.10$ | $1.00$ | $0.33$ | $0.05$ |

$$Gscv_1 = scv_1 \,\|\; Gscv_2 = scv_2 \,\|\; Gscv_3 = scv_3 \,\|\; Gscv_4 = scv_4\,\|\;Gscv_5 = scv_5 \,\|\; Gscv_6 = scv_6$$

### Type score

The interaction type score takes into account the diversity of interaction types reported for an interaction.

$$
\begin{aligned}
    S_t  &\equiv \text{Type Score}  \in [0,1]\\
    S_t (\text{cv}_i) &= \log _{(b+1)}(a+1)\\
    a &= \sum(scv_i \times n_i)\\
    b &= a + \sum(\max(Gscv_i))
\end{aligned}
$$

As in the method score, $scv\_i$ is a normalized score between 0 and 1, in this case associated to an interaction type CV term. An MI-type ontology term without an assigned score inherits the score from the nearest parent. Interaction-type scores are also customizable but by default they have assigned a heuristic score based on the assessment of the HUPO PSI–MI consortium:

| $cv\_i$ | $cv\_1$ | $cv\_2$ | $cv\_3$ | $cv\_4$ | $cv\_5$ | $cv\_6$ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Name | genetic interaction | colocalization | association | physical association | direct interaction | Unkwown |
| MI Id | MI:0208 | MI:0403 | MI:0914 | MI:0915 | MI:0407 | Unkwown |
| $scv\_i$ | $0.10$ | $0.33$ | $0.33$ | $0.66$ | $1.00$ | $0.05$ |

$$Gscv_1 = scv_1 \,\|\; Gscv_2 = scv_2 \,\|\; Gscv_3 = scv_3, scv_4, scv_5$$

More details including examples of how to use MIscore are available in PMID: [25652942](http://europepmc.org/article/MED/25652942). The code is fully available in the [MISCORE GitHub repository](https://github.com/MICommunity/miscore).
