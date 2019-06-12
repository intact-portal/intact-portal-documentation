# 3. Initiating curation – Publication Level

On starting curation of a paper the curator needs to ‘claim ownership’ of the publication by going to the “CURATE” section → Create a new publication → enter the PMID → Auto-complete.

Most details \(Journal, year of publication, author-list\) will be added automatically, but the curator will need to add:

* Manually add the corresponding author’s email address
* Select a “Dataset” - if appropriate.
* Assign the “Curation Depth” as IMEx or MIMIx
* Give the entry an IMEx ID if appropriate by clicking on the &lt;assign IMEx ID&gt; button.

#### This is an example of a completed Publication level page

![](../../.gitbook/assets/0%20%288%29.png)

## 

## 3.1 Duplication of Effort Avoidance

When the curator enters a publication for curation within the editor, a check is made in IMExCentral to ascertain whether the publication has been curated, or reserved for curation, by another partner database. If so, a message will tell the curator that this is the case. If another database has curated, or reserved, the publication already it is strongly recommended that the publication is not redundantly curated. If the curator still decides to curate the paper, an IMEx ID will not be issued.

If the publication is already curated within IntAct, the curator will be taken to the curated entry by the editor.

## 3.2 Publication annotations

Along with the common annotations described above, a publication may have any of the following annotations.

### 3.2.1 data-processing

This topic may be added at publication level where the data-processing description is common to _**all**_ the experiments \(_See Experiment Annotations_ section for further info and examples\). Briefly, this annotation topic is used to describe the steps in processing of data to obtain the _**identifiers**_ described in the entry. This annotation topic is visible in the public database.

### 3.2.2 contact-email

Usually this is the contact given in the publication. When there are many corresponding authors the contact emails for correspondence can be added in the same line as a **comma** \(not semi-colon\) separated list without spaces_._ Example: _john@ebi.ac.uk,doe@ebi.ac.uk_. Please make sure you do not add any space, or extra symbols.

### 3.2.3 contact-comment

Example:

“The original address given in the publication was john@doe.com. This address is now invalid and has been replaced by that given in contact-email. The original address is stored here.”

This topic can also be used to indicate that the contact email is absent from the publication. This annotation topic is not viewed on the public database.

### 3.2.4 experimental modification

Experimental details are entered where experiments have a protocol that is **non-standard**, and cannot be easily entered elsewhere. This annotation is only added at the Publication level when the modification\(s\) applies to **ALL** Experiments. More commonly this term is used at the **Experiment** level, specifically for that experiment.

### 3.2.5 curation depth

Curators should indicate whether the entry has been curated to IMEx or MIMIx depth \(see Section 1.2\)

![](../../.gitbook/assets/1%20%284%29.png)

### 3.2.6 dataset \(NA-MIMIx\)

This annotation topic should be used to link various publications pertaining to a particular topic of interest.

You should ADD your publication to a relevant Dataset\(s\), if the paper contains interactions relating to that Dataset\(s\) - as listed below.

To do this click on the relevant Dataset, click on ADD, then SAVE. This will add the Dataset annotation to **every** experiment.

If you wish to create a NEW Dataset, please get approval for this first.

For further info regarding Datasets see:

[http://www.ebi.ac.uk/intact/resources/datasets](http://www.ebi.ac.uk/intact/resources/datasets)

A list of Datasets to which you can add publications:-

| Cancer | Interactions investigated in the context of cancer |
| :--- | :--- |
| Alzheimers | Interactions investigated in the context of Alzheimers disease |
| Chromatin | Chromatin - Epigenetic interactions resulting in chromatin modulation |
| Cyanobacteria | Interaction dataset based on Cyanobacteria proteins and related species |
| Archaea | Interaction dataset based on Archaea proteins |
| Synapse | Interactions of proteins with an established role in the presynapse |
| Apoptosis | Interactions involving proteins with a function related to apoptosis |
| Parkinsons | Interactions investigated in the context of Parkinsons disease |
| Diabetes | Interactions investigated in the context of Diabetes |
| Affinomics | Interactions curated for the Affinomics consortium |
| NDPK | Interactions involving proteins containing InterPro domain IPR001564, Nucleoside diphosphate kinase, core |
| Cardiac | Interactions involving cardiac related proteins |
| Virus | Publications including interactions involving viral proteins |
| Neurodegeneration | Publications depicting interactions involved in neurodegenerative diseases. |
| Ulcerative colitis | Publications depicting interactions of proteins identified as having a link to ulcerative colitis |
| Crohns disease | Publications depicting interactions of proteins identified as having a link to Crohn's disease |
| Huntington's | Publications describing interactions involved in Huntington's disease |
| IBD - Inflammatory bowel disease | Publications depicting  interactions of proteins identified as having a link to IBD |
| PDBe | Data obtained from the Protein Data Bank Europe by automatic import. Do not add manually added crystal papers to this dataset. |

Do not add primary publications to dataset ‘PDBe’. These is reserved for direct imports from PDBe.

### 3.2.7 on-hold

Any experiment that is annotated with this topic will not be released to the public. This annotation is used to exclude submitted data which has not been published and integration of the data into IntAct is ‘in progress’. This annotation should only be used when really necessary and the reason for the entry being on-hold should be entered in the free text box

**Note:** Subsequent to release of the PubMed ID or the completion of the entries from a PubMed ID the ‘on-hold’ annotation **must** be deleted. Experiments **will not** be released automatically after the date has passed.

This annotation topic is not viewed on the public database.

### 3.2.8 author-submitted

This refers to the data added to entries submitted by the author directly to IntAct prior to publication. The format of the free text field should strictly be as follows: _YYYY-MM-DD: J Doe, University of place_.

| **Experiment AC** | **Description** |
| :--- | :--- |
| EBI-6476263 | 2012-09-27: M Boxem, Utrecht University |
| EBI-6430623 | 2012-12-05: M Meier, IMTEK, University of Freiburg |

## 3.3 Publication cross-references \(Xref\) and cross-reference qualifiers

All added Cross references must have a qualifier which usually needs to be added manually. The primary reference will be added automatically at the publication level as part of the Auto-complete process.

### 3.3.1 PubMed ID \(PMID\)

* * * 1. This cross-reference is given the qualifier ‘primary-reference’, as it is the primary source of data in an entry. The journal details will be added to an entry when the PMID is used to create an entry, and the ‘Auto-complete’ button pressed. The PMID and any IMEx XRef will be carried over to any subsequent Experiments, as each Experiment within an entry is created.

3.3.1.2 Unpublished Data or data lacking a PMID

When the data has been submitted prepublication and a PubMed ID can only be assigned at a later date ‘pubmed’ should be the primary-reference and the primary ID column should be filled in with ‘[unassignedxxx](about:blank), qualifier ‘primary-reference’. On publication if a PubMedID is not available then DOI cross-reference may be used with qualifier ‘primary reference’.

### 3.3.2 IMEx ID

IMEx IDs can be added to any paper curated to IMEx standards by members of the IMEx consortium, which have not previously been claimed as an IMEx record by another consortium member. The addition of an IMEx ID will automatically trigger the assignment of the IMEx identifiers on all the experiments with the same Primary Pubmed Reference and all of the associated interactions. This accession is of the form IM-XXXXX. The qualifier will normally be IMEx-primary, unless an entry already has an IMEx ID, in which case a second number \(which references the same entry\) may be added with the qualifier ‘imex-secondary’. If an entry does not yet have a PMID, the IMEx ID must be added manually.

