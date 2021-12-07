# Querying ChEMBL RDF

[prev](README.md)

<script>
  function toggleAnswer(id) {
  var answer = document.getElementById(id);
  if (answer.style.visibility === "hidden" ||
      answer.style.visibility === "none") {
    answer.style.visibility = "visible";
  } else {
    answer.style.visibility = "hidden";
  }
}
</script>


## Introduction
ChEMBL is a manually curated database of bioactive molecules with drug-like properties. It brings together chemical, bioactivity and genomic data to aid the translation of genomic information into effective new drugs. Built upon the ChEMBL database, an RDF representation of the ChEMBL database is produced by the European Molecular Biology Laboratory - European Bioinformatics Institute (EMBL-EBI) and provided for [download](https://www.ebi.ac.uk/rdf/services/sparql). The ChEMBL RDF model uses a basic internal ontology, called the ChEMBL Core Ontology (CCO), to identify all of the primary entities (e.g., Documents, Assays, Substances, Targets) in the ChEMBL database. The department of Bioinformatics (BiGCaT) at Maastricht University took the initiative to host the RDF and expose it to the scientific community through a SPARQL endpoint where queries can be executed against the RDF to find answers to biological questions. The tool is available through https://chemblmirror.rdf.bigcat-bioinformatics.org/.

## Figure of RDF schema
![Graphical representation of RDF schema](chembl_18_rdf_summary.png "ChEMBL RDF")
## Exercises

### Exercise 1 - Listing of subjects

**Listing chemicals**

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX dbpedia2: <http://dbpedia.org/property/>
PREFIX dbpedia: <http://dbpedia.org/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

PREFIX cco: <http://rdf.ebi.ac.uk/terms/chembl#>
SELECT ?molecule
WHERE {
  ?molecule a ?type .
  ?type rdfs:subClassOf* cco:Substance .
} limit 20
```

**Listing targets**

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX dbpedia2: <http://dbpedia.org/property/>
PREFIX dbpedia: <http://dbpedia.org/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

PREFIX cco: <http://rdf.ebi.ac.uk/terms/chembl#>
SELECT ?target 
WHERE { 
  ?target a ?type . 
  ?type rdfs:subClassOf* cco:Target .
} LIMIT 20
```

**Listing ChEMBL sources**

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX dbpedia2: <http://dbpedia.org/property/>
PREFIX dbpedia: <http://dbpedia.org/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

PREFIX cco: <http://rdf.ebi.ac.uk/terms/chembl#>
SELECT ?Source ?Description
   WHERE {
   ?Source ?p cco:Source .
   ?Source dcterms:description ?Description
} LIMIT 100
```

### Exercise 2 - Counting of subjects
count chemicals
count chemicals with activity X
count chemicals of subgroup
count chemicals in pubmed ID Y


### Exercise 3 - More detailed exploration

**List all assays, target names and UniProt IDs for the drug Paracetamol (CHEBI:46195)**

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX dbpedia2: <http://dbpedia.org/property/>
PREFIX dbpedia: <http://dbpedia.org/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

PREFIX cco: <http://rdf.ebi.ac.uk/terms/chembl#>
PREFIX chembl_molecule: <http://rdf.ebi.ac.uk/resource/chembl/molecule/>
SELECT ?activityLabel ?assayType ?targetLabel ?uniprot
WHERE {

  ?activity a cco:Activity ;
		rdfs:label ?activityLabel;
		cco:hasMolecule chembl_molecule:CHEMBL46195 ;
		cco:hasAssay ?assay .

  ?assay cco:assayType ?assayType.
  ?assay cco:hasTarget ?target .
  
  ?target rdfs:label ?targetLabel.
  ?target cco:hasTargetComponent ?targetcmpt .
  ?targetcmpt cco:targetCmptXref ?uniprot .
  ?uniprot a cco:UniprotRef
}
```

**Get all assay, binding affinity type (Kd, Ki, IC50) and affinity value for all compounds targeting Thrombin protein (CHEMBL204)**

```sparql
PREFIX chembl: <http://rdf.ebi.ac.uk/terms/chembl#>
PREFIX cco: <http://rdf.ebi.ac.uk/terms/chembl#>
PREFIX chembl_molecule: <http://rdf.ebi.ac.uk/resource/chembl/molecule/>
PREFIX chembl_target: <http://rdf.ebi.ac.uk/resource/chembl/target/>

SELECT distinct ?assayLabel ?assayType ?molLabel ?bindingAffinityType ?value WHERE {

  ?assay  chembl:hasTarget chembl_target:CHEMBL204.
  
  ?activity chembl:hasAssay  ?assay.
  ?assay cco:assayType ?assayType.
  ?activity chembl:hasMolecule ?molecule .

  chembl_target:CHEMBL204 rdfs:label ?targetLabel.
  ?molecule rdfs:label ?molLabel.
  ?assay  rdfs:label ?assayLabel.
  
  ?activity chembl:type ?bindingAffinityType.
  ?activity chembl:standardValue ?value.

} limit 100
```

list chemicals that target protein X
list assays that measure activity of chemical Y
for journal X, list each paper and the number of chemicals in there

### Exercise 4 - Federated SPARQL query
For metabolites in WP X, which protein targets do the chemicals have?

### End
Thank you for your participation. For any feedback or questions about this section, please contact Ammar Ammar (a.ammar@maastrichtuniversity.nl).
