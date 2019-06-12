# Scoring

## How is the intact-miscore calculated?

The IntAct MI score is based on the manual annotation of every instance of a binary interaction \(A-B\) within the IntAct database. First all instances of the A-B interacting pair are clustered by accession number. Each entry has been annotated using the PSI-CVs and we use this information to score by the interaction detection method and by the interaction type. Additionally we count the number of publications the interaction has appeared in, up to a maximum of 8. Each of these variables is normalised between 0-1. The cumulative score is also normalised between 0-1 across the entire IntAct database, with 1 representing an interaction in which we have the highest confidence.





