The IntAct Molecular Interactions database provides its data in 4 different data interchange formats, PSI-MI XML, PSI-MI TAB, MI-JSON and XGMML while terms are defined in the [PSI Molecular Interactions Controlled Vocabulary](https://www.ebi.ac.uk/ols/ontologies/mi). Below are links to our schemas and some content explanations. For more information on how to use our data, please see our [User Guide](https://www.ebi.ac.uk/intact/documentation/user-guide).

# Molecular Interaction Formats

An overview of schemas and full details for all xml and tab-delimited formats and our CV can be found on the [HUPO Proteomics Standards Initiative Molecular Interactions (PSI-MI) Group page](https://www.psidev.info/groups/molecular-interactions)

## PSI-MI XML

The PSI-MI XML (MI-XML, MIF) data interchange format is an XML-based molecular interactions format. The version currently used by IntAct when returning results in XML are the PSI-MI XML 2.5 and 3.0 versions. Documentation is available in the [HUPO-PSI GitHub repository](https://github.com/HUPO-PSI/miXML) and the [PSICQUIC GitHub repository](https://psicquic.github.io/PSIMIXML.html).

## PSI-MI TAB (miTab)

The PSI-MI TAB data interchange format is a common tab-delimited molecular interactions format. IntAct currently supports PSI-MITAB 2.5 and PSI-MITAB 2.7, documentation is available in the [HUPO-PSI GitHub repository](https://github.com/HUPO-PSI/miTab) and the [PSICQUIC GitHub repository](https://psicquic.github.io/PSIMITAB.html)

## MI-JSON

The MI-JSON data interchange format provides the core interaction data, including all binding features, in a more concise format than PSI-MI XML for use cases where the XML files are too large to transfer in a reasonable amount of time. It removes the following content:

- some free-text annotations

- interactor cross-references, while it retains the interaction cross-references

- interactor aliases, such as gene names, secondary UniProt IDs

The schema and full details can be found in the [MI Community GitHub repository](https://github.com/MICommunity/psi-jami/tree/master/jami-interactionviewer-json)

Use case: [ComplexViewer](https://github.com/MICommunity/ComplexViewer)

## RDF

RDF is a standard model for data interchange on the Web. Here we list the RDF formats supported in IntAct, with links provided for each format specifications document:

* RDF/XML and RDF/XML-ABBREV \([RDF Syntax Recommendation](https://www.w3.org/TR/rdf-syntax-grammar/)\)
* N3 \([Tim Berners-Lee's Notation 3 Language](https://www.w3.org/TeamSubmission/n3/)\)
* N-Triples \([RDF Core's N-Triples Language](https://www.w3.org/TR/2014/REC-n-triples-20140225/)\)
* Turtle \([Terse RDF Triple Language](https://www.w3.org/TR/2014/REC-turtle-20140225/)\)

## BioPAX

IntAct supports BioPAX Level 2 and Level 3. BioPAX \(Biological Pathway Exchange\) is a standard language to represent biological pathways at the molecular and cellular level. Additional information is available at [https://github.com/BioPAX/specification](https://github.com/BioPAX/specification).

## XGMML

The XGMML data interchange format is used for importing data from IntAct directly into network analysis software such as as [Cytoscape](https://cytoscape.org/). Documentation for the XGMML format is available in [Wikipedia](https://en.wikipedia.org/wiki/XGMML). IntAct has developed its own [Cytocsape App](https://apps.cytoscape.org/apps/intactapp) for querying IntAct data directly from Cytoscape.

# Controlled Vocabulary (CV)

The CV for the annotation of molecular interaction, **Proteomics Standards Initiative for Molecular Interaction Controlled Vocabulary (PSI-MI CV)**, has been developed within the HUPO Proteomics Standards Initiative (HUPO-PSI).

The CV can be navigated at the [Ontology Lookup Service (OLS)](https://www.ebi.ac.uk/ols/ontologies/mi).

New terms can be requested via its [GitHub repository](https://github.com/HUPO-PSI/psi-mi-CV). 
