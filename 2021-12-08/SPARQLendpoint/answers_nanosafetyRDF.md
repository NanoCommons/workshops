### Exercise 1 - listing of subjects

```SPARQL
select distinct ?KE where { 
    ?s nci:C25492 ?KE .
}
```

### Exercise 2 - counting of subjects
A - ERM ids

```SPARQL
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX dcterms: <http://purl.org/dc/terms/>

SELECT (COUNT(DISTINCT ?id as ?nid)) WHERE { 
    ?s a obo:CHEBI_59999 ; 
         dcterms:identifier ?id.
} 
```
B - publications

```SPARQL
SELECT (COUNT(DISTINCT ?doi as ?ndoi)) WHERE { 
    ?source a wd:Q13442814 ; 
              owl:sameAs ?doi .
} 
```

C - endpoints

```SPARQL
SELECT (COUNT(DISTINCT ?ep as ?nep)) WHERE { 
    ?o a bao:BAO_0000179 ;
       rdfs:label ?ep .
} 
```
  
### Exercise 3 - going one step further
  
  ```SPARQL
select distinct ?doi ?ep  where {
  ?s obo:BFO_0000056 ?mg ;
     dcterms:source ?source .
  ?source owl:sameAs ?doi .
  ?mg obo:OBI_0000299 ?o .
  ?o a bao:BAO_0000179 ;
       rdfs:label ?ep .

} ORDER BY ?doi
  ```
  
### Exercise 4 - extracting values

A
```SPARQL
PREFIX nsvoc: <https://ammar257ammar.github.com/RDFied-datasets/nanosafery_vocabulary:>
PREFIX bao: <http://www.bioassayontology.org/bao#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX sio: <http://semanticscience.org/resource/>
PREFIX enm: <http://purl.enanomapper.net/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX wd: <http://www.wikidata.org/prop/direct/>
PREFIX owl: <http://www.w3.org/2002/07/owl#>

select distinct ?mlabel ?doi ?measurement ?value where {
  ?s rdfs:label ?mlabel ; 
     obo:BFO_0000056 ?mg .
  ?s dcterms:source ?source .
  ?source owl:sameAs ?doi .
  ?mg obo:OBI_0000299 ?o .
  ?o a bao:BAO_0000179 ;
       rdfs:label ?measurement ;
       rdfs:label "shape"@en .
  optional{?o sio:has-value ?value. }

} 
```

B 
  ```SPARQL
PREFIX nsvoc: <https://ammar257ammar.github.com/RDFied-datasets/nanosafery_vocabulary:>
PREFIX bao: <http://www.bioassayontology.org/bao#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX sio: <http://semanticscience.org/resource/>
PREFIX enm: <http://purl.enanomapper.net/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX wd: <http://www.wikidata.org/prop/direct/>
PREFIX owl: <http://www.w3.org/2002/07/owl#>

select distinct ?mlabel ?doi ?measurement ?medium ?value_range ?value ?unit  where {
  ?s rdfs:label ?mlabel ; 
     obo:BFO_0000056 ?mg .
  ?s dcterms:source ?source .
  ?source owl:sameAs ?doi .
  ?mg obo:OBI_0000299 ?o .
  ?o a bao:BAO_0000179 ;
       rdfs:label ?measurement ;
       rdfs:label "zeta potential"@en .
  optional{?o obo:STATO_0000035 ?value_range .}
  optional{?o sio:has-value ?value. }
  optional{?o sio:has-unit ?unit .}
  optional{?o enm:has-condition ?g .}
  optional{?g rdfs:label ?medlabel
              ; sio:has-value ?medium .}

} ORDER BY ?mlabel, ?doi
  ```
  
  
### Exercise 5 - Federated query & BONUS question 

  Get names of KEs based on ids through federated query to AOP wiki
  
  ```SPARQL
  PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX aopo: <http://aopkb.org/aop_ontology#>
PREFIX sio: <http://semanticscience.org/resource/>
PREFIX ncbitaxon: <http://purl.bioontology.org/ontology/NCBITAXON/>

select distinct ?mie ?mietitle ?aop ?ao ?aotitle where {
    ?s a obo:CHEBI_59999;
    dcterms:identifier ?ID ;
    dcterms:title ?materialname ;
    dcterms:type ?materialtype ;
    sio:SIO_000636 ?mie.
SERVICE <https://aopwiki.rdf.bigcat-bioinformatics.org/sparql>{
?mie dc:title ?mietitle.
?aop aopo:has_molecular_initiating_event ?mie; aopo:has_adverse_outcome ?ao.
?ao dc:title ?aotitle;ncbitaxon:131567 "WCS_9606".}
 }
 ```
