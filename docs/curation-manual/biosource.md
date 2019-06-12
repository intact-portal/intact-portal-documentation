# 8. BioSource

The BioSource is used for:

* Host Organism of the experiment
* Expressed in \(Biosource used for expressing the participant\)
* Interactor Organism: the Organism from which the interactor originates

A Biosource may be any of the following:

a\) An organism \(tissue/cell line unspecified\) Example: _Homo sapiens_

b\) A tissue type, which includes cell suspensions derived from tissues.

c\) A cell line

d\) in vitro

N.B. in the IntAct editor ‘Cell type’ denotes ‘Cell line’.

## 8.1. How to create a new BioSource/Host Organism

In practise this only needs to be done if an organism is not currently listed on the drop-down menu for “Host Organism” – most common organisms are already present.

From the publication or Experiment level, click on Main → New → Organism

The main source for organism information is http://www.uniprot.org/taxonomy/

Add the NCBI Tax Id of the new organism e.g. 40324 \(for _Stenotrophomonas maltophilia_\), and enter it in NCBI Tax Id field in the IntAct editor.

Press ‘Auto-complete’, and the other fields should be filled in. \(short label is “stema” taken from the UniProt “Mnemonic”/5 letter organism identifier, and the UniProt Xref should have qualifier set as ‘identity’.\)

Then Save.

## 8.2 How to create a Cell or Tissue Type

There are two stages to this:-

First, check the cell line or tissue is NOT present in the Biosource drop-down menu already - so SEARCH for it in the editor.

If the cell line/tissue is not currently present in the editor

Select Main → New → CV object/

Then Select ‘Cell Type’ or ‘Tissue’ – as appropriate

Click Create

![](../../.gitbook/assets/0%20%283%29.png)

**Shortlabel:** Add the name of cell line/tissue \(in lowercase letters and using underscores instead of spaces\)

**Fullname:** Repeat the name of cell line/tissue and add a very brief description

Then add an **Xref or Annotation**:

_Tissue_:

Database = “Brenda”

Identifier = “tissue identifier” \(BTO:xxxxxxxx\) or EFO

Qualifier = “Identity”

[http://www.brenda-enzymes.info/ontology/tissue/tree/update/update\_files/BrendaTissueOBO](http://www.brenda-enzymes.info/ontology/tissue/tree/update/update_files/BrendaTissueOBO)

or

[http://www.ebi.ac.uk/ols/ontologies/bto](http://www.ebi.ac.uk/ols/ontologies/bto)

or

[http://www.uniprot.org/docs/tisslist.txt](http://www.uniprot.org/docs/tisslist.txt)

_Cell Type \(immortalised cell line\):_

**Cabri** or other Database:

Database = “Cabri” or other appropriate DB

Identifier = “Cabri or other DB identifier”

Qualifier = “Identity”

**ATCC cell lines**:

Do NOT add as Xref, but

Annotation topic = “url”

Description = “url of entry”\(if you cannot do either of these, add the catalogue number as a Annotation topic = “comment”.\)

AND add an annotation \(comment\) giving further info about the cell line.

To locate your cell line in Cabri/ATCC it is probably easiest to do a Google search such as “293 cabri” or “293 atcc”.

Some cell lines are now present in Brenda.

![](../../.gitbook/assets/1%20%283%29.png)

![](../../.gitbook/assets/2%20%282%29.png)

Link this new cell type/tissue to a BioSource. If you do not, you will not be able to see it on the Host-Organism drop-down menu.

Select Main → New → Organism

Enter the TaxID of the species this cell line/tissue belongs to

Click on Auto Fill

Short-label: ‘Species-name of cell line/tissue’ e.g. ‘human-293. Use underscores instead of spaces in the cell type/tissue name.

Fullname: Repeat the name of cell line/tissue and add a very brief description, e.g. Human epitheloid cervix carcinoma HeLa cells.

Add either the Cell type \(cell lines\) OR Tissue \(tissue or primary cells\) from the drop-down list near the bottom of the page

NB: Start the species name with upper case, unless there's a good reason not to. Do not add a full-stop at the end of the full name.

Save

![](../../.gitbook/assets/3%20%281%29.png)

The new cell line/tissue should now appear on the Host organism drop-down menu and can be used in an experiment.

### 8.2.1 Tissues vs cell lines

There can be confusion as to what constitutes a ‘tissue’. For the purposes of the IntAct database, tissue includes primary cells which have been directly derived from an organism, then passaged to provide a single cell type. A ’tissue’ will usually have an entry in either the Brenda tissue ontology \([https://www.brenda-enzymes.info/ontology/tissue/tree/update/update\_files/BrendaTissueOBO](https://www.brenda-enzymes.info/ontology/tissue/tree/update/update_files/BrendaTissueOBO) or [https://www.ebi.ac.uk/ols/ontologies/bto](https://www.ebi.ac.uk/ols/ontologies/bto)\) or UniProtKB tissue list: [http://www.uniprot.org/docs/tisslist.txt](http://www.uniprot.org/docs/tisslist.txt)

When a specific cell type cannot be found in either list, use the closest term available and add the detailed description in the ‘exp-modification’ annotation on experiment.

Example: colonic circular smooth muscle – add as \(Tissue\) ‘circular smooth muscle’ and add ‘colon’ as an exp mod.

Examples: blood, aortic smooth muscle, adipocyte, melanoma, neuron

An embryo becomes a foetus when organogenesis commences and the dpc \(days post coitum\) of the organism should be considered when using these terms.

In the case of a specific bacterial strain, take the strain name from UniProtKB species list: [http://www.uniprot.org/docs/speclist.txt](http://www.uniprot.org/docs/speclist.txt) or [http://www.uniprot.org/taxonomy](http://www.uniprot.org/taxonomy/).

## 8.3 Cell Type

#### Immortalised cell lines are referred to as ‘cell types’ in IntAct.

### 8.3.1 Re-classified cell lines

If a cell line has been re-classified or proven to be contaminated it must be annotated to the corrected BioSource.  
Example: In [EBI-367374](http://www.ebi.ac.uk/intact/search/do/hvWelcome?searchString=EBI-367374) \(PMID:15109305\) the authors state that KB cells were used in the experiment. Subsequently these cells have been re-classified as a HeLa sub-clone \(See definition in CABRI database\). Therefore, the BioSource for this experiment must be entered as HeLa cells and a note in the annotation under ‘CAUTION’ to explain the discrepancy.

**8.4 Special cases**

In the case of host organism for Y2H assays, it was agreed to use the top level hierarchical yeast term \(yeasx TaxID:4932\), but if a yeast protein was identified as an interactor, this should be mapped to the correct strain or reference proteome.

In the case of a crystal, the host organism is always taken as the crystallisation solution i.e.’in vitro’ even in the case of a homomultimer.

