# Querying the Nanosafety RDF

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

Adverse Outcome Pathways (AOPs) have been proposed to explore interactions of chemicals/materials with biological systems. Each AOP starts with a molecular initiating event (MIE) and possibly ends with adverse outcome(s). So far, we do not fully understand how many nanomaterials interact with proteins, biomembranes, cells, and biological structures in general. There is limited insight into the toxicology-related key events (KEs) they trigger, such as oxidative stress and inflammation, or the biological processes underlying these KEs. For this SPARQL endpoint we integrate the annotation of nanomaterials and their MIEs with ontology annotation to demonstrate how we can then query AOPs and biological pathway information for these materials. 

## Figure of RDF schema

<figure>
    <img src="NSRDF.png" alt="A kitten">
    <figcaption>Graphical representation of the Resource Description Framework Schema for nanomaterials (NMs)<figcaption>
<figure>  


## Exercises

### Exercise 1 - listing of subjects
This first exercise is about creating simple SPARQL queries that count particular types of subjects in the RDF. See the example SPARQL query below that counts the number of Key Events in the RDF.

```SPARQL
PREFIX sio: <http://semanticscience.org/resource/>

select distinct ?KE where { 
    ?s sio:SIO_000001 ?KE .
}
```

When copying this SPARQL query and executing it, you will see the KE id's that are mentioned in the Nanosafety RDF. Of course these are hard to interpret. In the RDF schema you can see that the RDF also contains an MIE/KE text. This is the name of the KE as mentioned in the paper.

Modify the above query to select the MIE/KE text. Which predicate do you use: - <button onclick="toggleAnswer('q1')">Answer</button><span id="q1" style="visibility: hidden">nci:C25492</span>

### Exercise 2 - counting of subjects

Count the number of distinct ERM identifiers

HINT: use COUNT(DISTINCT ?id as ?nid)

```SPARQL
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX dcterms: <http://purl.org/dc/terms/>

SELECT (COUNT(DISTINCT ?id as ?nid)) WHERE { 
    ?s a obo:CHEBI_59999 ; 
         dcterms:identifier ?id.
} 
```
