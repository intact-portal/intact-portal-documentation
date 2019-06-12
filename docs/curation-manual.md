# 1. IntAct

\*\*\*\*

IntAct provides a freely available, open source database system and analysis tools for molecular interaction data. All interactions are derived from literature curation or direct user submissions. There are 2 database instances: PROD \(production\) and TEST \(test\). Curators add or edit data into the production database via the production editor. The test database is used to test new updates of the database and editor before putting them on production editor. Large-scale data is always uploaded first on the test editor to ensure correct representation.

### 1.1 IntAct data model

Data curated in IntAct may be from peer reviewed publications, submitted pre-publication data or data submitted by authors as an extension of data related to a previous publication.

The IntAct data model is built on the following concepts:

* An entry is a publication or pre-publication.
* One publication contains one-to-many experiments;
* One experiment has one-to-many interactions;
* One interaction has one-to-many participants.

![](../.gitbook/assets/1.png)

A Participant is an Interactor plus its features.

Interactors can be proteins/peptides, genes, nucleic acids, or small molecules.

A participant can have none-to-many features.

Features: these further describe the component of the interaction e.g. region of protein used, PTM present on the protein involved in the interaction, mutations or a tag.

### 1.2 Curation Depth

Curation can be carried out at two levels: IMEx \(e.g. PMID:22453911\) or MIMIX \(minimum information for interaction exchange level \(e.g. PMID:17687370\).

The MIMIx rules can be found here: [http://www.nature.com/nbt/journal/v25/n8/box/nbt1324\_BX1.html](http://www.nature.com/nbt/journal/v25/n8/box/nbt1324_BX1.html)

The IMEx rules can be found at: [http://www.imexconsortium.org/sites/imexconsortium.org/files/documents/imex\_curation\_rules.pdf](http://www.imexconsortium.org/sites/imexconsortium.org/files/documents/imex_curation_rules.pdf)

IMEx IDs are assigned from IMEx Central \([https://imexcentral.org/icentralbeta/](https://imexcentral.org/icentralbeta/)\), which the editor accesses to assign an IMEx ID. Once an IMEx ID has been assigned, the paper should either be completed in full or, if this subsequently proves impossible, a comment should be added to the publication record in IMEx Central explaining why not. Once an IMEx ID has been assigned, it cannot be removed from the paper in IMEx Central.

#### Brief Summary of IMEx vs MIMIx Curation

| **IMEx** | **MIMIx** |
| :--- | :--- |
| Capture all PPI experimental data in publication - includes colocalisations but NOT genetic interactions |  |
| **Publication** |  |
| PMID + autocomplete | PMID + autocomplete |
| Author contact details | Author contact details |
| IMEx designator | MIMIx designator |
| Dataset |  |
| **Experiment** |  |
| Host organism-tissue/cell | Host organism-tissue/cell |
| Interaction Detection method | Interaction Detection method |
| Participant Detection method | Participant Detection method |
| Additional annotation – experimental modification, data processing |  |
| **Interaction** |  |
| Interaction Type | Interaction Type |
| Figure legend\(s\) | Figure legend\(s\) |
| Additional annotation – Comments, Caution |  |
| Location xref \(GO\) – usually only colocalisations |  |
| **Participants** |  |
| Experimental/Biological role | Experimental/Biological role |
| Expressed in \(in vitro expts only\) |  |
| Features – tags, radio/isotope labels, deletion mutants, point mutations |  |
| Binding site xrefs \(InterPro\) |  |

In the subsequent rules ‘NA-MIMIX’ will be used as a tag to indicate that this annotation need not be added to a MIMIX level entry.

### 1.3 Controlled Vocabulary terms

IntAct uses the HUPO-PSI Controlled Vocabulary \(CV\) for interaction detection, Participant Detection, feature detection method, feature type, Interaction type, interactor type, database, interactor roles, and cross-reference types. The ontology lookup service \(OLS\) provides an overview of various PSI \(CV\) terms [https://www.ebi.ac.uk/ols/ontologies/mi](https://www.ebi.ac.uk/ols/ontologies/mi).

If an adequate term to describe the methods used in the publication is not available in the current CV hierarchy, a new CV term should be requested by creating an issue at the PSI-MI GitHub site: [https://github.com/HUPO-PSI/psi-mi-CV/issues](https://github.com/HUPO-PSI/psi-mi-CV/issues). Alternatively, an email to [intact-help@ebi.ac.uk](mailto:intact-help@ebi.ac.uk) can be sent.

In cases where the controlled vocabulary term is pending, choose a possible parent of the requested term, give a description of the method used by the authors under annotation topic ‘exp-modification’ and a ‘remark-internal’- ‘Revisit when CV in place’. We run a periodic clean-up of the pending CV terms.

Additional annotation terms used by IntAct are available from ftp://[ftp.ebi.ac.uk/pub/databases/intact/current/cv/](http://ftp.ebi.ac.uk/pub/databases/intact/current/cv/).

### 1.4 Accession numbers

Each IntAct object is given an accession number \(EBI-xxxxxxx\), automatically generated by the editor. If a change is made which involves the transfer of contents from an entry to a new IntAct object, with the original IntAct object being deleted, then the accession number of the old IntAct object will be cross-referenced in the new IntAct object using the Reference Qualifier ‘intact-secondary’. This will ensure that the correct record/s is/are pulled up using both the former and the more recent accession numbers.

### 1.5 Short Label

Each IntAct object is given a mandatory short label. These use lowercase letters, numbers and special characters such as underscore \(\_\), hyphen \(-\) and space. Any other characters are replaced by \(\_\) underscore. There is a character limit of 256 on the Short Label. Whenever possible, short labels will be generated by the editor.

### 1.6 Full Name

Each IntAct object may be given an optional full name. The character limit on the full name is 1000 characters, and standard keyboard characters are allowed.

### 1.7 Annotation

Annotations are additional free text information which can be added to IntAct objects. They can be added at the level of Publication, Experiment, Interaction, Interactor or Feature. Again, only standard keyboard characters are allowed. Annotations are added under a series of specified headings – many of which are restricted to a particular level of an entry. Specific annotation will be detailed at the appropriate level, but the following may be added at any level

#### 1.7.1 comment

This annotation topic can be used to describe additional information which cannot fit under other annotation topics. It is desirable that the comments are restricted to as few as possible and are complete sentences, and do not contain unusual \(publication-specific\) abbreviations as comments are visible externally.

| **Interaction AC** | **Description** |
| :--- | :--- |
| EBI-6512836 | The binding of the isolated FADD death domain to LRRK2 was weak. |
| EBI-6555250 | Levels of H4K17Ac at the promoter level of this gene increased in UpSET \(Q9VUB5\) -/- cells |
|  EBI-2658579 | Atrx, but not Hira, is specifically required for H3.3 enrichment at telomeres. H3.3 colocalization with telomeres is lost in Atrx-null ESCs, but maintained in Hira -/- ESCs. |

#### 1.7.2 remark-internal

This annotation topic may be added at publication level if there is a common remark to be made about the entire publication. It can be added at Experiment and/or Interaction level – wherever is most appropriate.

‘remark-internal’ is for internal use only and is not made publicly available so comments and/or messages to oneself or other curators can be made here.

The remark-internal can be deleted if it is no longer appropriate.

This topic may also be used to describe why certain experiments described in a publication were not annotated. Some examples of ‘remark-internal’ used \(at Publication level\) are:

| Did not curate Fig 3a/b/c \(Kinase Assay\) as LRRK2 was not purified other than by IP. |
| :--- |
| Awaiting reply from author - email sent 4/2/14 |
| I am not sure if I entered all the co-localizations correctly? |
| Ang 3 in this paper must be UniProt Ang-4... |
| There is NO mention of an anti-HA antibody in the paper - so participant detection entered as "WB" rather than "anti-tag WB". |
| From Fig 7 I have entered the one mutation result stated to have statistical significance. \(text states \(fig 7a +B\): "The G2019S, R1441C and I2020T mutations each enhanced binding of LRRK2 to MKK6," ??! |

#### 1.7.3 caution

This is used for warning the user:

* about possible errors or for specifying grounds for confusion.
* in experiments where the author has expressed misgivings about a technique while comparing with another described in the same or different paper.
* where there may be some [difference](http://thesaurus.reference.com/browse/ambiguity) in the sequence noted by the author and that present in the UniProtKB entry or method identification carried out by the curator.

| **Interaction AC** | **Description** |
| :--- | :--- |
| EBI-2363999 | A single band appears in the Rpt 2/3/4/5 identification region but the authors does not give an actual identification to this protein and it cannot be assigned from the image on the gel. |
| EBI-2939789 | PMRT5 amino acids numbers have had +1 added to agree with UniProt sequences. |
| EBI-2464773 | The PDB accession numbers given at the end of the paper for this crystal appear to be incorrect. |
| EBI-3505028 | One IPI identifier was mapped to CDK2AP1 by the author, whereas in fact it mapped to CDK2AP2 |
| EBI-2928481 | Mutant Mdm2 \(minus N terminal amino acids\) does bind to p53 in Fig 2A, yet it does NOT bind p53 as shown in Fig 6E. |
| EBI-4373956 | The cell type in which this interaction occurred was not specified. |
| EBI-5351142 | myc-CREPT rather than flag-CREPT is stated to have been used in the figure legend. |
| EBI-6267663 | Binding region length is given as 1101-1640 in the text. As the known length of the protein is 1460, it has been assumed that two digits have been reversed. |
| EBI-5326135 | The molecule "TCF4" is the protein "Transcription factor 7-like 2" \(Q9NQB0 \(TF7L2\_HUMAN\)\) whose Gene ID has a synonym of TCF4. |

