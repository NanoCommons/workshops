## Nanosafety RDF

Adverse Outcome Pathways (AOPs) have been proposed to explore interactions of chemicals/materials with biological systems. Each AOP starts with a molecular initiating event (MIE) and possibly ends with adverse outcome(s). So far, we do not fully understand how many nanomaterials interact with proteins, biomembranes, cells, and biological structures in general. There is limited insight into the toxicology-related key events (KEs) they trigger, such as oxidative stress and inflammation, or the biological processes underlying these KEs. For this SPARQL endpoint we integrate the annotation of nanomaterials and their MIEs with ontology annotation to demonstrate how we can then query AOPs and biological pathway information for these materials. 

```SPARQL
PREFIX sio: <http://semanticscience.org/resource/>

select distinct ?KE where { 
    ?s sio:SIO_000001 ?KE .
}
```

QUESTION 1:

Modify the above query to select the MIE/KE text. Which predicate do you use:

select distinct ?KE where { 
    ?s nci:C25492 ?KE .
}

QUESTION 2:

Count the number of distinct ERM identifiers

HINT: use COUNT(DISTINCT ?id as ?nid)


PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX dcterms: <http://purl.org/dc/terms/>

SELECT (COUNT(DISTINCT ?id as ?nid)) WHERE { 
    ?s a obo:CHEBI_59999 ; 
         dcterms:identifier ?id.
} 
