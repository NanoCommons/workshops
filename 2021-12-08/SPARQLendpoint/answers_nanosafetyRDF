### Exercise 1 - listing of subjects

```SPARQL
select distinct ?KE where { 
    ?s nci:C25492 ?KE .
}
```

### Exercise 2 - counting of subjects

```SPARQL
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX dcterms: <http://purl.org/dc/terms/>

SELECT (COUNT(DISTINCT ?id as ?nid)) WHERE { 
    ?s a obo:CHEBI_59999 ; 
         dcterms:identifier ?id.
} 
```
  
### Exercise 3 - 
  
  ```SPARQL
  select distinct ?measurement where {
  ?s obo:BFO_0000056 ?mg .
  ?mg obo:OBI_0000299 ?o .
  ?o a bao:BAO_0000179 ;
       rdfs:label ?measurement .
}
  ```
  
### Exercise 4 - : 6 TiO2 NP A (anatase/rutile) with a value of -8.92 +/- 0.75   
  
  ```SPARQL
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
  
  
### Exercise 5 - 

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
