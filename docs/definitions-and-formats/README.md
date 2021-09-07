The IntAct Molecualr Interactions database provides its data in 3 different file formats, PSI-MI XML, PSI-MI TAB and MI-JSON. Below are links to our schemas and some content explanations. For more information on how to use our data, please see the [User Guide](https://wwwdev.ebi.ac.uk/intact/beta/documentation/user-guide).

## PSI-MI XML & PSI-MI TAB (miTab)

### Schema

The schemas and full details for all version of these format can be found [here](https://www.psidev.info/groups/molecular-interactions)

## MI-JSON

### Schema

The schema and full details are found [here](https://github.com/MICommunity/psi-jami/tree/master/jami-interactionviewer-json)

### Notes

The MI-JSON provides the core interaction data, including all binding features, in a more concise format than PSI-MI XML for use cases where the XML files are too large to transfer in a reasonable amount of time. It removes the following content:

- some free-text annotations

- interactor cross-references, while it retains the interaction cross-references

- interactor aliases, such as gene names, secondary UniProt IDs

Use case: [ComplexViewer](https://github.com/MICommunity/ComplexViewer)
