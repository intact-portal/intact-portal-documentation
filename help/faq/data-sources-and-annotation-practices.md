# Data Sources and Annotation Practices

## Where does Intact data come from?

That's a tough question but thankfully, our team is on it. Please bear with us while we're investigating.

## How do I submit data to IntAct?

Answer

## What advantages does it have to submit data to IntAct?

Yes, after a few months we finally found the answer. Sadly, Mike is on vacations right now so I'm afraid we are not able to provide the answer at this point.

## Why does the number of interactions given in a particular high-throughput paper, differ from the number I can download from IntAct from the same publication?

Answer

## Are all the molecules reported in an interaction directly binding?

Answer: No, not all the interactions represented in IntAct can be considered as direct binary contacts between the molecules involved. In fact, most of the experimental interaction data that we curate does not allow to say whether an interaction is direct or not. 

The 'Interaction type' column can help you find out if an interacting pair is directly binding. We distinguish three major types of interaction:

* \*\*\*\*[**Direct interaction**](https://www.ebi.ac.uk/ols/ontologies/mi/terms?iri=http%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FMI_0407): Interaction that happens between molecules that are in direct contact with each other. We reserve this annotation for evidence found through methods that use purified molecules, not cell extracts or other complex samples, so we can 100% sure that there are no undetected participants bridging the interaction \(e.g. the structure of two co-crystallized, purified proteins\). Enzymatic reactions, curated exclusively when using purified participants, fall under this category, but we use interaction types depicting the specific reaction \(e.g. a [phosphorylation reaction](https://www.ebi.ac.uk/ols/ontologies/mi/terms?iri=http%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FMI_0217)\).
* \*\*\*\*[**Physical association**](https://www.ebi.ac.uk/ols/ontologies/mi/terms?iri=http%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FMI_0915): Interaction between molecules within the same physical complex, complex being defined as a group of molecules that are physically in contact at the same point in time. A physical association **does not imply a direct contact**, even if it refers to an interaction with only two participants. The annotation implies they are together in the same complex, but there could be undetected participants that bridge the interaction, so no proof of directness is given. Physical associations typically refer to interactions with two participants, but can sometimes involve more. 
* \*\*\*\*[**Association**](https://www.ebi.ac.uk/ols/ontologies/mi/terms?iri=http%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FMI_0914): Interaction between molecules that may participate in formation of one, but possibly more, physical complexes. The experimental evidence behind the interaction does not allow to determine if one of more interacting complexes are being detected. That is, alternative combinations of interacting molecules are possible. An association always has more than two participants, even though [spoke-expanded](../../docs/expansion-method.md) associations may appear as expanded binaries in our results table. 



