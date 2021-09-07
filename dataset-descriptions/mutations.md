# Mutations

[This dataset](ftp://ftp.ebi.ac.uk/pub/databases/intact/current/various/mutations.tsv) contains annotations of experimental evidence where mutations have been shown to affect a protein interaction.

Several types of mutations are captured and the terms used to described them can be found in the [PSI-MI controlled vocabulary](https://www.ebi.ac.uk/ols/ontologies/mi).

## Dataset Description

* Mutation \(MI:0118\): A change in a sequence or structure in comparison to a reference entity due to a insertion, deletion or substitution event. _This root term is used when there is a mutation present in a protein and the wild type version has not been tested or shown to interact in the referenced paper._
  * Mutation causing an interaction \(MI:2227\): A change in a sequence or structure in comparison to a reference entity due to a insertion, deletion or substitution event that enables an interaction when compared with the wild-type, which does not interact.
  * Mutation decreasing interaction \(MI:0119\): Region of a molecule whose mutation or deletion decreases significantly interaction strength or rate \(in the case of interactions inferred from enzymatic reaction\).
    * Mutation decreasing interaction rate \(MI:1130\): Region of a molecule whose mutation or deletion decreases significantly interaction rate \(in the case of interactions inferred from enzymatic reaction\).
    * Mutation decreasing interaction strength \(MI:1133\): Region of a molecule whose mutation or deletion decreases significantly interaction strength.
  * Mutation disrupting interaction \(MI:0573\): Region of a molecule whose mutation or deletion totally disrupts an interaction strength or rate \(in the case of interactions inferred from enzymatic reaction\). • Mutation disrupting interaction rate \(MI:1129\): Region of a molecule whose mutation or deletion totally disrupts an interaction rate \(in the case of interactions inferred from enzymatic reaction\). • Mutation disrupting interaction strength \(MI:1128\): Region of a molecule whose mutation or deletion totally disrupts an interaction strength. 
  * Mutation increasing interaction \(MI:0382\): Region of a molecule whose mutation or deletion increases significantly interaction strength or rate \(in the case of interactions inferred from enzymatic reaction\).
    * Mutation increasing interaction rate \(MI:1131\): Region of a molecule whose mutation or deletion increases significantly interaction rate \(in the case of interactions inferred from enzymatic reaction\).
    * Mutation increasing interaction strength \(MI:1132\): Region of a molecule whose mutation or deletion increases significantly interaction strength.
  * Mutation with no effect \(MI:2226\): A change in a sequence or structure in comparison to a reference entity due to a insertion, deletion or substitution event that does not have any effect over an interaction when compared with the wild-type.
  * Mutation with complex effect \(MI:2333\): A change in a sequence or structure in comparison to a reference entity due to a insertion, deletion or substitution event that has a complex effect over the interaction when compared with the wild-type. A complex effect is such that cannot be described in increasing, decreasing, causing, disrupting or no effect terms.

## Output format description

We provide a tab-delimited flatfile download with the full dataset. Every instance of a mutation affecting a given interaction is given a unique identifier \(_“Feature AC”_\). Please notice that some mutations will affect more than one residue position range in non-consecutive order. Each one of these non-consecutive ranges is recorded in a separate line, hence there will always be a difference between the number of lines in the file and the number of unique mutations. Here is a brief description of the different columns used in the file:

* Feature AC: Accession number for that particular mutation feature.
* Feature short label: Human-readable short label summarizing the amino acid changes and their positions, compliant with the Human Genome Variation Society recommendations \(see [http://varnomen.hgvs.org/recommendations/protein/](http://varnomen.hgvs.org/recommendations/protein/)\) .
* Feature range\(s\): Position\(s\) in the protein sequence affected by the mutation.
* Original sequence: Wild type amino acid residue\(s\) affected, in one letter code.
* Resulting sequence: Replacement sequence \(or deletion\) in one letter code.
* Feature type: Mutation type, following the PSI-MI controlled vocabularies as stated above.
* Feature annotation: Specific comments about the feature that can be of interest.
* Affected protein AC: Affected protein identifier \(preferably UniProtKB accession, if available\).
* Affected protein symbol: As given by UniProtKB.
* Affected protein full name: As given by UniProtKB.
* Affected protein organism: TaxID and species name as given by UniProtKB.
* Interaction participants: Identifiers for all participants in the affected interaction, along with their species and molecule type between brackets.
* PubMedID: Reference to the publication where the interaction evidence was reported.
* Figure legend: Reference to the specific figures in the paper where the interaction evidence was reported.
* Interaction AC: Interaction accession within our databases. This can be used to obtain further information about the interaction.

Further columns will be added once the dataset is enriched with cross-references to other databases such as UniProt and Ensembl. We plan to provide mappings to genomic coordinates in the near future.

## Mutations dataset format example

| Feature AC | Feature short label | Feature range\(s\) | Original sequence | Resulting sequence | Feature type | Feature annotation | Affected protein AC | Affected protein symbol | Affected protein full name | Affected protein organism | Interaction participants | PubMedID | Figure legend | Interaction AC |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| EBI-1203484 | P20659:p.Asp3702\_Tyr3703delinsAlaAla | 3702-3703 | DY | AA | mutation decreasing strength\(MI:1133\) |  | uniprotkb:P20659 | TRX | Histone-lysine N-methyltransferase trithorax \(EC 2.1.1.43\) \(Lysine N-methyltransferase 2A\) | 7227 - Drosophile melanogaster \(Fruit fly\) | uniprotkb:P20659 \(protein, 7227 - Drosophile melanogaster \(Fruit fly\)\) | 10656681 | 5A | EBI-1203452 |
| EBI-709274 | O43521:p.Leu152Glu | 152-152 | L | E | mutation decreasing\(MI:0119\) |  | uniprotkb:O43521 | B2L11 | Bcl-2-like protein 11 \(Bcl2-L-11\) \(Bcl2-interacting mediator of cell death\) | 9606 - Homo sapiens | uniprotkb:O43521\(protein, 9606 - Homo sapiens\);uniprotkb:P97287\(protein, 10090 - Mus musculus\) | 15694340 |  | EBI-709266 |
| EBI-10762087 | P69411:p.Pro116\_Gly117insXaa | 116-117 | PG | PXG | mutation\(MI:0118\) | comment:Feature - insertion of crosslinkable amino acid p-benzoyl-L-phenylalanine \(pBpa\) | uniprotkb:P69411 | RCSF | Outer membrane lipoprotein RcsF | 83333 - Escherichia coli \(strain K12\) | uniprotkb:P69411 \(protein, 83333 - Escherichia coli \(strain K12\)\);uniprotkb:P0A940 \(protein, 83333 - Escherichia coli \(strain K12\)\) | 25525882 | Fig. 2C Supp Fig.3D | EBI-10761554 |

