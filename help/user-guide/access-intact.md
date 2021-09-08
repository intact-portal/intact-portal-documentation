# Data Access Options

IntAct provides a number of different ways to access its data:

## Website

Users can create bespoke, manual searches directly through the [website](www.ebi.ac.uk/intact). For help with getting started, please consult the [Quick Guide to searching IntAct](https://github.com/intact-portal/intact-portal-documentation/blob/master/help/user-guide/searching-intact.md).

## Webservice

IntAct provides a range of different [webservices](https://github.com/intact-portal/intact-portal-documentation/blob/master/technical-corner/apis.md).

## Download

Download the data via our [ftp server](https://www.ebi.ac.uk/intact/download#ftp) or access bespoke [datasets](https://www.ebi.ac.uk/intact/documentation/datasets) directly.

## PSICQUIC Service

IntAct provides its data through the bespoke [PSICQUIC](http://www.ebi.ac.uk/Tools/webservices/psicquic/view/main.xhtml) webservice for molecular interactions data. PSICQUIC queries data from a number of providers using the [PSI-MI TAB (miTab) format](https://www.ebi.ac.uk/intact/documentation/docs#definitions_formats) and returns its results per providers, e.g. IntAct, MINT, MENTHA. 

Details on the data provided by each service can be found in the [PSICQUIC registry](http://www.ebi.ac.uk/Tools/webservices/psicquic/registry/registry?action=STATUS). All PSICQUIC data providers should support MITAB2.5.

More information about PSICQUIC can be found on the [PSICQUIC GitHub project page](https://psicquic.github.io/)

## Cytoscape

The bespoke [Cytoscape IntAct App](https://apps.cytoscape.org/apps/intactapp) lets users query IntAct directly through Cytoscape and create Molecular Interaction networks within Cytoscape.

IntAct App provides 2 entry points for building these networks:
- Fuzzy Search: create big networks for concepts, e.g. Kinase, "Cell cycle", etc.
- Exact Query: create small to medium networks for (lists of) specific sets of molecules, e.g. brca1, tp53, etc.

## Use direct links

### 1. Link directly to a search result using a string:

Example: search for interactions for gene name ["ncd80"](https://www.ebi.ac.uk/intact/search?query=Ndc80).

Example: search for interactions for UniProt ID ["P40460"](https://www.ebi.ac.uk/intact/search?query=P40460).

Example: search for interactions for publication [11179222](https://www.ebi.ac.uk/intact/search?query=11179222).

### 2. Link directly to an interaction AC:

Example: interaction [EBI-1003164](https://www.ebi.ac.uk/intact/details/interaction/EBI-1003164)
