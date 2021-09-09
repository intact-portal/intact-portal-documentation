# Usage

## Can I search for more than one protein at a time?

Yes. The [Batch Search](https://www.ebi.ac.uk/intact/home#batch-search) allows you to search for multiple proteins simultaneously in IntAct. Either paste a list of search terms directly into the box or upload a plain text file containing the list of terms. We recommend the use of common identifiers like UniProtKB ACs or gene names. In the following step, the Batch Search attempts to resolve the query terms and allows you to select the terms you want to use in the actual search. IntAct will retrive interactions containing interactors matching these terms.

## The results of my search contain mixed species e.g. human-mouse interactions – why, and how do I remove them?

The data reflects how the authors performed the original experiments. In many cases genes from one species are exogenously expressed in a second, for example a tagged mouse protein is expressed in a human cell line, resulting in _mouse-human_ _interactions_. It is our practice to collate the data as it was observed in the experiment e.g. _human-mouse_, _mouse-rat_ and let the user decide whether to infer _human-human_ or _mouse-mouse_ _interactions_ from these observations. Of course, some of the data is _host-pathogen_, and the mixed species interaction is valid _in vivo_.

The species folder on the IntAct ftp site contains species-specific datasets in [PSI-XML2.5](ftp://ftp.ebi.ac.uk/pub/databases/intact/current/psi25/species/) and [PSI-XML3.0](ftp://ftp.ebi.ac.uk/pub/databases/intact/current/psi30/species/) formats. These files also contain mixed species interactions.

To retrieve data for a specific species, search for its [NCBI taxon ID](https://www.uniprot.org/taxonomy/), e.g. 9606 for human. On the results page, use the `Interactor Species` filter and, using the toggle button in the top right corner of the pop-up window, select if you want to retrieve any interactions containing at least one interactor of your choice of organism or only interactors of your choice of organism.

![image](https://user-images.githubusercontent.com/10517124/132673663-5c46816a-ff28-4c1e-8639-e3a4971e2a1e.png)

We precompute [interactomes](https://www.ebi.ac.uk/intact/interactomes) for 16 bespoke species.

## I want to look for interactions between pathogen and host proteins, can I find this information in IntAct?

Yes. Use the search for a single organism above and in the `Interactor Species` filter select both organisms.

## I submitted a list of 2000 UniProtKB accession numbers via the "search" interface of IntAct, I obtain "0 binary interactions found for search term", why and how do I find results to my search?

The problem is the length of the query. It is difficult to provide a specific limit, because it is defined according to the length in characters that your query consists of, and that depends on the type of identifier you are using. If you submit a list of space-separated UniProtKB accessions, the limit is approximately **700** identifiers in search. This also applies to [PSCIQUIC view](www.ebi.ac.uk/Tools/webservices/psicquic/view/main.xhtml) and PSICQUIC-based Cytoscape import tool.

## I have found no interactions for my protein rat Zap70. How do I find if a homolog/ortholog/paralog with a high degree of sequence similarity has any interactions in the IntAct database?

Go to [www.ebi.ac.uk/tools/sss](https://github.com/intact-portal/intact-portal-documentation/tree/8e742af7316018e9ef02c904bd4a4b7932e7cafc/help/faq/www.ebi.ac.uk/tools/sss/README.md)

Select your Search Engine of choice e.g. NCBI-BLAST.

Click on protein then paste your sequence into the box, make any required changes to the parameters, add your e-mail address and Submit.

![](../../.gitbook/assets/image.png)


You will receive the results in tabular form, with additional hyperlinks through to other databases containing information about this protein. You can see below that, although IntAct contains no molecular interactions for rat it does for mouse and human


![image](https://user-images.githubusercontent.com/77560653/132332415-f1e3b27e-5c7d-4c97-a163-83f9f50f65f2.png)


![image](https://user-images.githubusercontent.com/77560653/132333470-954b0af3-25e7-4ab2-9f88-68614133307a.png)



IntAct results can be found in Molecular Interactions cluster. Press on the link to access the data in IntAct

![image](https://user-images.githubusercontent.com/77560653/132332515-acd7ff82-bdea-427c-9581-88f8a2eeab2c.png)

## How do I find if there are interactions involving a specific domain or region in my protein of interest?

IntAct annotates the binding region of interacting proteins at the feature level. Allowing the users to query for binding regions using InterPro accession numbers is still a work in progress.

## How do I find interactions affected by variant or mutant forms of my protein?

Interactions affected by mutations can be visualized by selecting the “Affected by Mutation” option found on the left side of the network view. Alternatively, you can download the “Mutations” dataset [here](https://www.ebi.ac.uk/intact/download#dataset_files)

![image](https://user-images.githubusercontent.com/77560653/132435272-dbd69e4a-38c6-45ce-90b2-aef6793a421c.png)


## Does IntAct record isoform-specific interactions?

Yes, IntAct curators stringently specify the protein isoform or the pro-chain as mentioned by the authors by using appropriate UniProtKB accession number. You can query using UniProtKB for the isoforms or make use of auto-suggestion option in the quick search mode

![image](https://user-images.githubusercontent.com/77560653/132434908-58a995f3-875c-445c-bccd-57c679d6c393.png)


## Can I find drug-target interactions in IntAct?

Yes, IntAct has captured molecular iteraction of proteins with drugs and other small molecules using appropriate ChEBI accession number. Small molecules include entities which are synthetic or modified peptides but not those directly encoded by the genome.

![image](https://user-images.githubusercontent.com/77560653/132433884-41bc3285-2c69-4855-b822-82d82d37e859.png)


## Can I find interactions between different molecule types in IntAct? (e.g. protein-DNA interactions)

Interacting partner(s) in IntAct database can be of different molecular types such as proteins, small molecules, nucleic acids, complexes and genes. Based on the type of partner, interactions between protein-protein, protein-DNA and protein-RNA, protein-gene, RNA-RNA, protein-small molecule, protein-macromolecule complex interactions are well documented in IntAct.

![image](https://user-images.githubusercontent.com/77560653/132434006-7b5636cb-d04f-4c84-b2ea-5ec99e12899b.png)


## How to link to the IntAct website?

Detailed access options for IntAct are discussed in our [User Guide](https://wwwdev.ebi.ac.uk/intact/beta/documentation/user-guide).

## Why do I get fewer results when I search IntAct via the PSICQUIC service, than when I search on the IntAct website?

The IntAct PSICQUIC webservice only contains interactions curated by IntAct curators while all entries curated by [IMEx](http://www.imexconsortium.org/) curators are available through the IntAct homepage. To see entries curated by external curators in the IntAct environment (for example MINT or UniProtKB), or from other IMEx partners select the results from their PSICQUIC service. All PSICQUIC data providers should support MITAB2.5.
