# Advanced/MIQL Search

This will help you in using our feature - [Advanced/MIQL Search](https://www.ebi.ac.uk/intact/home#advanced-search)

## Advanced/MIQL Syntax

* Use OR or space ' ' to search for ANY of the terms in a field, enclosed within brackets ()

* Use AND if you want to search for those interactions where ALL of your terms are found, enclosed within brackets ()

* Use quotes (") if you look for a specific phrase (group of terms that must be searched together) or terms containing special characters that may otherwise be interpreted by our query engine (eg. '-' in idA or idB) 

* Use '-' as a field value to specify that the field can be null or absent

* Use parenthesis for complex queries (e.g. '(XXX OR YYY) AND ZZZ')

* Wildcards (*,?) can be used between letters in a term or at the end of terms to do fuzzy queries,
but never at the beginning of a term 

* Optionally, you can prepend a symbol in from of your term.

    * \+ (plus): include this term. Equivalent to AND. e.g. +P12345
    * \- (minus): do not include this term. Equivalent to NOT. e.g. -P12345
    * Nothing in front of the term. Equivalent to OR. e.g. P12345


## Advanced/MIQL fields

| Field Name | Searches On | Example |
| :--- | :--- | :--- |
| idA | Identifier A | [idA:P74565](https://www.ebi.ac.uk/intact/search?query=idA:P74565) |
| idB | Identifier B | [idB:P74565](https://www.ebi.ac.uk/intact/search?query=idB:P74565) |
| id | Identifiers (A or B) : Alternate ids included | [id:P74565](https://www.ebi.ac.uk/intact/search?query=id:P74565) |
| alias | Aliases (A or B) | [alias:(KHDRBS1 OR HCK)](<https://www.ebi.ac.uk/intact/search?query=alias:(KHDRBS1 OR HCK)>) |
| identifier | Identifiers and Aliases undistinctively | [identifier:P74565](https://www.ebi.ac.uk/intact/search?query=identifier:P74565) |
| pubauth | Publication 1st author(s) | [pubauth:scott](https://www.ebi.ac.uk/intact/search?query=pubauth:scott) |
| pubid | Publication Identifier(s) | [pubid:(10837477 OR 12029088)](<https://www.ebi.ac.uk/intact/search?query=pubid:(10837477 OR 12029088)>) |
| taxidA | Tax ID interactor A: be it the tax ID or the species name | [taxidA:mouse](https://www.ebi.ac.uk/intact/search?query=taxidA:mouse) |
| taxidB | Tax ID interactor B: be it the tax ID or species name | [taxidB:9606](https://www.ebi.ac.uk/intact/search?query=taxidB:9606) |
| species | Species. Tax ID A or Tax ID B | [species:human](https://www.ebi.ac.uk/intact/search?query=species:human) |
| type | Interaction type(s) | [type:"physical association"](<https://www.ebi.ac.uk/intact/search?query=type:"physical association">) |
| detmethod | Interaction Detection method(s) | [detmethod:"two hybrid"](<https://www.ebi.ac.uk/intact/search?query=detmethod:"two hybrid">) |
| interaction_id | Interaction identifier(s) | [interaction_id:EBI-761050](https://www.ebi.ac.uk/intact/search?query=interaction_id:EBI-761050) |
| pbioroleA | Biological role(s) interactor A | [pbioroleA:enzyme](https://www.ebi.ac.uk/intact/search?query=pbioroleA:enzyme) |
| pbioroleB | Biological role(s) interactor B | [pbioroleB:enzyme](https://www.ebi.ac.uk/intact/search?query=pbioroleB:enzyme) |
| pbiorole | Biological role(s) interactor (A or B) | [pbiorole:enzyme](https://www.ebi.ac.uk/intact/search?query=pbiorole:enzyme) |
| ptypeA | Interactor type A | [ptypeA:protein](https://www.ebi.ac.uk/intact/search?query=ptypeA:protein) |
| ptypeB | Interactor type B | [ptypeB:protein](https://www.ebi.ac.uk/intact/search?query=ptypeB:protein) |
| ptype | Interactor type (A or B) | [ptype:protein](https://www.ebi.ac.uk/intact/search?query=ptype:protein) |
| pxrefA | Interactor xref A | [pxrefA:"GO:0005794"](https://www.ebi.ac.uk/intact/search?query=pxrefA:"GO:0005794") |
| pxrefB | Interactor xref B | [pxrefB:"GO:0005794"](https://www.ebi.ac.uk/intact/search?query=pxrefB:"GO:0005794") |
| pxref | Interactor xref (A or B) | [pxref:"GO:0005794"](https://www.ebi.ac.uk/intact/search?query=pxref:"GO:0005794") |
| xref | Interaction xref(s) | [xref:"GO:0005634"](https://www.ebi.ac.uk/intact/search?query=xref:"GO:0005634") |
| annot | Annotations/Tags Interaction | [annot:"imex curation"](<https://www.ebi.ac.uk/intact/search?query= annot:"imex curation">) |
| udate | Last update of the interaction | [udate:[20210607 TO 20220906]](<https://www.ebi.ac.uk/intact/search?query=udate:[20210607 TO 20220906]>) |
| negative | Boolean value which is true if an interaction is negative | [negative:true](https://www.ebi.ac.uk/intact/search?query=negative:true) |
| complex | Complex Expansion method(s) | [complex:spoke](https://www.ebi.ac.uk/intact/search?query=complex:spoke) |
| ftypeA | Feature type(s) A | [ftypeA:"binding region"](<https://www.ebi.ac.uk/intact/search?query=ftypeA:"binding region">) |
| ftypeB | Feature type(s) B | [ftypeB:"binding region"](<https://www.ebi.ac.uk/intact/search?query=ftypeB:"binding region">) |
| ftype | Feature type(s) (A or B) | [ftype:"binding region"](<https://www.ebi.ac.uk/intact/search?query=ftype:"binding region">) |
| pmethodA | Participant identification method(s) A | [pmethodA:"western blot"](<https://www.ebi.ac.uk/intact/search?query=pmethodA:"western blot">) |
| pmethodB | Participant identification method(s)) B | [pmethodB:"western blot"](<https://www.ebi.ac.uk/intact/search?query=pmethodB:"western blot">) |
| pmethod | Participant identification method(s) (A or B) | [pmethod:"western blot"](<https://www.ebi.ac.uk/intact/search?query=pmethod:"western blot">) |
| stc | Boolean value to know if Interactor A or B has stoichiometry information. | [stc:true](https://www.ebi.ac.uk/intact/search?query=stc:true) |
| param | Boolean value to know if the Interaction has some parameters. | [param:true](https://www.ebi.ac.uk/intact/search?query=param:true) |
| geneName | Gene name for Interactor A or B | [geneName:brca2](https://www.ebi.ac.uk/intact/search?query=geneName:brca2) |
| source | Source database(s) | [source:mbinfo](https://www.ebi.ac.uk/intact/search?query=source:mbinfo) |
| intact-miscore | IntAct MI Score (between 0 and 1), based on number of publications, detection methods and interaction types. | [intact-miscore:[0.5 TO 1.0]](<https://www.ebi.ac.uk/intact/search?query=intact-miscore:[0.5 TO 1.0]>) |
| altidA | Alternate ids A search | [altidA:ensemblfungi:YDR334W](https://www.ebi.ac.uk/intact/search?query=altidA:ensemblfungi:YDR334W) |
| altidB | Alternate ids B search | [altidB:ensemblfungi:YFL039C](https://www.ebi.ac.uk/intact/search?query=altidB:ensemblfungi:YFL039C) |
| aliasA | Aliases A | [aliasA:KHDRBS1](https://www.ebi.ac.uk/intact/search?query=aliasA:KHDRBS1) |
| aliasB | Aliases B | [aliasB:HCK](https://www.ebi.ac.uk/intact/search?query=aliasB:HCK) |
| pubyear | Publication year | [pubyear:[2012 TO 2022]](<https://www.ebi.ac.uk/intact/search?query=pubyear:[2012 TO 2022]>) |
| pubauthors | Any author from the list | [pubauthors:Sviderskiy](https://www.ebi.ac.uk/intact/search?query=pubauthors:Sviderskiy) |
| taxidHost | Host organism : be it the tax ID or species name| [taxidHost:9606](https://www.ebi.ac.uk/intact/search?query=taxidHost:9606) |
| rdate | Released date | [rdate:[20110607 TO 20220906]](<https://www.ebi.ac.uk/intact/search?query=rdate:[20110607 TO 20220906]>) |
| mutation | Effected by mutation Either by mutationA or mutationB | [mutation:true](https://www.ebi.ac.uk/intact/search?query=mutation:true) |
| mutationA | Effected by mutation by mutationA | [mutationA:true](https://www.ebi.ac.uk/intact/search?query=mutationA:true) |
| mutationB | Effected by mutation Either by mutationB | [mutationB:true](https://www.ebi.ac.uk/intact/search?query=mutationB:true) |
| geneNameA | Gene name for Interactor A | [geneNameA:XRCC3](https://www.ebi.ac.uk/intact/search?query=geneNameA:XRCC3) |
| geneNameB | Gene name for Interactor B | [geneNameB:brca2](https://www.ebi.ac.uk/intact/search?query=geneNameB:brca2) |
