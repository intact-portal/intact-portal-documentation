# 10. Special Cases

### 10.1 Prepublication or submitted data

Data submitted by an author prior to publication has the highest priority in the curation pipeline. Confidentiality is critical in these cases. The data submitted by the author should be stored at $PRO6/intact/local/data/curation-materials/year directory in a separate directory with the format firstauthor-year, for example smith-2010.

### 10.1.1 Creating a publication, lacking a PMID in the editor

\(Note, this is normally only required for handling direct submissions or pre-publication papers\)

Press button labelled ‘Curate’

Select ‘Create a new publication’

Select ‘Create entry \(unassigned\)

![](../../.gitbook/assets/0%20%286%29.png)![](../../.gitbook/assets/1%20%281%29.png)

An empty entry will be created with an ‘unassignedxxx’ identifier in place of the PMID.

 An IMEx accession number also needs to be associated with the entry.

Log on at [https://imexcentral.org/icentralbeta/user](https://imexcentral.org/icentralbeta/user)

* * * 1. Select ‘Add’

![](../../.gitbook/assets/2%20%281%29.png)![](../../.gitbook/assets/3%20%282%29.png)

Add details of the authors and the eventual publication from the submission. ‘Add’ the paper to the database.

![](../../.gitbook/assets/4%20%281%29.png)

On the next screen, assign an IMEx ID.

* * * 1. ![](../../.gitbook/assets/5.png)
      2. Transfer this IMEx ID back onto the entry in the IntAct editor. The database will be ‘imex’, the primary ID the IMEx accession number and the qualifier will be ‘imex-primary’. Then create the first experiment in the normal manner.
      3. Two additional annotations should be added at the publication level.
      4. 1. ‘submitted’ with the annotation in the format:
         1.  ‘2004-09-10: JS Choudhary, The Wellcome Trust Sanger Institute, Hinxton, UK’
         2. **2. ‘on-hold’ added to the experiment**. The experiment may be checked and accepted after curation, however the on-hold remains until the authors give us a written permission to make the data public or the publication containing the data is released by the journal. At this point the on-hold should be removed, the correct PubMed ID should be assigned \(if available\) and the accuracy of the data should be checked with respect to the public paper. The journal, year, author list etc. may be filled up using autocomplete while entering the PubMed ID.

Once the entry is complete, check with the authors that the data is the way they would like it to appear. This is normally done by the curator in charge of the entry. When the author contacts the curator to make the data public or the paper is in the public domain the entry may be released using the unassigned number, a DOI or PubMed ID. If only the DOI is available this becomes the primary-reference. When the PubMedID is available the PubMedID now becomes the primary reference and the DOI qualifier is changed to ‘see-also’

A request should also be made to the submitter for inclusion of the following sentence in the publication:

_‘The protein interactions from this publication have been submitted to the IMEx \(http://www.imexconsortium.org\) consortium through IntAct \[x\] and assigned the identifier IM-xxxxx.'_

X. PMID: 24234451

If the data is submitted by the author post online publication but prior to publication of the print version, confidentiality does not have to be maintained and a request for inclusion of the above sentence referring to the references to IntAct and IMEx accession numbers in the final publication should still be made.

### 10.2. Importing interaction data from other databases

If an interaction is imported from another database \(Example: KIAA and Riken\) put the accession number or reference number for that interaction from the source database in the interaction annotation cross-references. Do not just add the URL of the source database.

### 10.3 Annotating data from partially curated source

This data was obtained from sources other than the original publication. There are currently only two examples of this – an early FlyNet and a PDBe import.

FlyNet consisted of a set of binary interactions, linked to a single experiment from a single holding publication. The papers these interactions came from were added as xrefs on the interaction. If you curate a paper Aug 2005 or earlier which contains drosophila proteins, check the PMID. If it brings up an interaction attached to the jacq-2005-1, \(EBI-866743, unassigned4\), it is part of the FlyNet set. If you curate the paper, delete the PMID xref from the FlyNet interaction and, if it is the only xref on that specific interaction, delete the interaction as well.

Any entry marked with the dataset PDBe has structural wwPDB data imported from PDBe. This contains all the information pertaining to the structural studies from the publication; however other experimental data contained within the publication is not covered and needs to be manually annotated. When annotating these papers do the following:

1. Remove the dataset annotation on the Publication page.

2. Derive stoichiometry from the publication and add this to the interactors.

3. Check that the features and sequences are appropriately represented in the interaction.

4. Add any additional experiments.

5. Add an IMEx ID \(assuming the entry is now of IMEx standard\).

### 10.4 Unpublished data submitted by the author as an extension of published data

Occasionally authors ask us to hold additional information which was not included in a particular publication but was generated by the same methodology. The original publication where the methodology and some data have been published must be curated in IntAct before curating the additional data.

Where such additional data is being curated the annotation topics ‘submitted’, ‘url’, ‘data-processing’ must be filled in where appropriate. An annotation ‘caution’ must be added with the description that reads as follows:

 ‘The data described by this entry is not part of an independent publication and contains data produced as an extension of the work described in PMID: xxxxxxx using the methodology described therein.’.

This type of data will not have a PMID, it will retain the ‘unassigned1234” identifier in its place. The original article should be cross-referenced with its PMID and a reference qualifier see-also.

### 10.5 Handling Amended Large Datasets

#### 10.5.1 When the error is by the database

* 1. **The data was correct but a subset is being withdrawn** \(e.g. a low confidence subset\). The interaction subset should be deleted. A Caution comment should be added to the experiment, and the original dataset may be made available at a static ftp site should the originating database wish. A news item/tweet should be made announcing this change. No change to the IMEx ID required.
  2. **The data was incorrect** – the interaction dataset \(and experiment if necessary\) should be deleted and replaced by a new dataset \(and experiment\). A Caution comment should be added to the experiment. A news item/tweet should be made announcing this change. The IMEx ID of the paper should not change but interaction IDs should be subsequent to the original set, rather than a repeated set. To avoid this problem, please import the new interactions before deleting the old ones, so the IMEx assigner will give them new, non-redundant IMEx IDs.

#### 10.5.2 When the error is by the author

1. **The erratum is published** – the publication should be entered as a separate entry with a new IMEx ID. If the original entry still contains data additional to that which has been withdrawn, it should be maintained with a Caution comment added to the publication, and the PMID/DOI and the IMEx ID of the new publication of the erratum added, using qualifier see-also. The erratum publication should have its own PMID/DOI as primary-reference, its unique IMEx ID as IMEx-primary, and the PMID/DOI and IMEx ID of the original paper as qualifier see-also. A news item/tweet should be made announcing this change.
2. **The author does not wish to publish the erratum.** The interaction dataset \(and experiment if necessary\) should be deleted and replaced by a new dataset \(and experiment\). A Caution comment should be added to the experiment. A news item/tweet should be made announcing this change. The IMEx ID of the paper should not change but interaction IDs should be subsequent to the original set, rather than a repeated set. To avoid this problem, please import the new interactions before deleting the old ones, so the IMEx assigner will give them new, non-redundant IMEx IDs.

### 10.6 Data represented more than once in the database

Data may be represented more than once in the database because it is shared between independent studies. If at all possible, try to avoid this situation unless it is a direct request from an author submitting data and you cannot persuade him/her that this is not a good idea. To enter such data, you need to identify the publication that is the primary source of the data. This could be done by contacting the author/s. The data on this primary publication alone must be considered for DR and CC line export. This data in all the other places should be attached to an experiment with the annotation ‘uniprot-dr-export: No’. The primary and subsidiary publications with the data should have a cross-reference to each other using database = “pubmed”, identifier = “PubMed id” and qualifier = “see-also”; and database = “intact”, identifier = “IntAct Accessions” and qualifier = “see-also”. Annotation topic = “comment” on the experiments must clearly describe the primary and subsidiary dataset.

Example: EBI-1256426, EBI-1190357

### 10.7 Curation request

Request for curating published work whether by the authors of the publication or scientist in the field should have the annotation topic ‘curation request’ with the annotation in the format:

‘2004-09-10: JS Choudhary, The Wellcome Trust Sanger Institute, Hinxton, UK’

### 10.8 Causal Interaction Annotation – draft annotation rules

Causality consists on an additional information than can be added to a physical interaction describing the effect that one molecule has on its binding partner \(for instance, the phosphorylation of MEK by ERK results in the activation of MEK\).

 Annotation of Causality is NOT mandatory in IMEx.

Causal Interactions can be captured \(in IMEx interactions\) only when they meet the following criteria:

1. The interaction is binary \[or can be exported as binary\].
2. Interactions to which this annotation is added should be ‘interaction type = direct’ \(or child terms\), with the exception of ‘Ch-IP’ and ‘mirna interference luciferase assay’.
3. Causality must be experimentally demonstrated in the same paper. Inferred causality, or references to external publications, should not be captured.
4. To define directionality, Participants need to have prerequisites to be annotated with biological roles:
   1. Modulator entity: regulator \(and children\) or enzyme
   2. Modulated entity: regulator target or enzyme target
5. Causality is an annotation captured at the Interaction level, using the annotation topic: ‘Causality Statement’
6. Causality statements will be made using the following controlled vocabulary, with NO additional text, copy/paste from the OLS is STRONGLY recommended \(for further detailed terms, please see also all the children of ‘causal statement’: [https://www.ebi.ac.uk/ols/ontologies/mi/terms?iri=http%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FMI\_2234](https://www.ebi.ac.uk/ols/ontologies/mi/terms?iri=http%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FMI_2234)\)

up-regulates

up-regulates activity

up-regulates quantity

 up-regulates quantity by expression

 up-regulates quantity by stabilization

down-regulates

down-regulates activity

down-regulates quantity

 down-regulates quantity by expression

 down-regulates quantity by stabilization

1. When an interaction results in a PTM being added to the substrate, capture this using the following syntax

Annotation topic ‘resulting-ptm’ free text Identifier amino acid-three letter code-residue number \[MOD CV term\]

e.g. P12345 ser-99 O-phospho-L-serine

**Example1: enzymatic assays**

\(interaction EBI-6994245, phosphorylation\)

PMID: [19424295](http://europepmc.org/abstract/MED/19424295), protein kinase A phosphorylates and activates Limk1

![](../../.gitbook/assets/6.png)

![](../../.gitbook/assets/7.png)

**Example2: mirna interference luciferase assay**

\(interaction EBI-21003080, physical association\)

PMID: [26031775](https://www.ebi.ac.uk/intact/editor/publication/EBI-21003051), miR-16 targets FEAT mRNA and induces its degradation

![](../../.gitbook/assets/8.png)

![](../../.gitbook/assets/9.png)

