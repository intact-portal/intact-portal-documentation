# APIs

We have following four web services catering for the web site, they are available as REST APIs, please find their details here.

1. IntAct Interactor Search
2. IntAct Interaction Search
3. IntAct Network Viewer
4. IntAct Data

## IntAct Interactor Search

This web service is for searching interactors in IntAct. It is used in the website to provide interactor suggestions while typing in search box and also to resolve interactors while doing batch search. You can find fine details for this REST api [here](https://www.ebi.ac.uk/intact/ws/interactor/swagger-ui.html). 

## IntAct Interaction Search

This web service is for searching binary interactions in IntAct database. It is used in the website to search for interactions on the basis of a search term typed in search box or while doing batch search. It also provides interactors participating in the interactions. You can find fine details for this REST api [here](https://www.ebi.ac.uk/intact/ws/interaction/swagger-ui.html)

## IntAct Network Viewer

This web service is for getting IntAct binary interactions and interactors in json format. It is used in the website to feed interaction network viewer in search results page. You can find fine details for this REST api [here](https://www.ebi.ac.uk/intact/ws/network/swagger-ui.html)

## IntAct Data

This web service is for having interface for IntAct data in our graph database. It is used in the website to export the data in various formats in search result page, to create solr indexing and to fetch the interaction details & interaction json(for viewer) in details page. You can find fine details for this REST api [here](https://www.ebi.ac.uk/intact/ws/graph/swagger-ui.html)

