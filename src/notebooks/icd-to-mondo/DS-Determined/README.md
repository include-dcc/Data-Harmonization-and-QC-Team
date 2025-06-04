# DS-Determined - Mapping ICD codes to Mondo

The initial ICD9/10 code mapping to Mondo was done using the file `CDM_extracted_ICD_codes.csv` 
in https://www.synapse.org/Synapse:syn63923531 and the notebook [here](https://github.com/include-dcc/Data-Harmonization-and-QC-Team/blob/main/src/notebooks/icd-to-mondo/Compare%20Xrefs%20-%20DS-Determined.ipynb) to find Mondo terms that have a corresponding ICD9/10 database cross-references.

Since there are many ICD codes in the data that are not found as a database cross-reference in Mondo we will use the ICD term labels as input to Harmonica to try to map these labels to Mondo terms. Any potential mappings found will be passed back to the Mondo team for review and addition into Mondo.
 
## ICD Sources
As part of the Mondo development process, ICD10CM is ingested and converted to OWL in the [mondo-ingest repo](https://github.com/monarch-initiative/mondo-ingest). The icd10cm.owl file in `src/ontology/components` will be used as the source for querying out the CURIEs and labels and term definitions from ICD10CM.

A suitable OWL source of ICD9 is needed.


## SPARQL Query
The query `get_icd10_labels.sparql` was used with [ROBOT](https://robot.obolibrary.org/) and run as:
`robot query -i icd10cm.owl -q get_icd10_labels.sparql data/icd10_labels.tsv`. 

## Mapping - Data Annotation
The `data/icd10_labels.tsv` file was filtered to contain only the ICD10 codes in the DS-Determined data that did not have an existing database cross-reference in Mondo. This file was then used as input to Harmonica to find matches to Mondo terms, initially based on the term label.


