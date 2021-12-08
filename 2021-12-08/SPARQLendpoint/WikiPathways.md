# Querying WikiPathways

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
WikiPathways (https://www.wikipathways.org) is a biological pathway database known for its collaborative nature and open science approaches. The road toward a sustainable, community-driven pathway database goes through integration with other resources such as Wikidata and allowing more use, curation and redistribution of WikiPathways content. The SPARQL endpoint allows the access of the WikiPathways RDF and integrate its content with other databases. The RDF contains all pathways, their datanodes (genes, proteins, metabolites, etc.), author information, molecular descriptors, and more.

The WikiPathways SPARQL endpoint is accessible on [https://sparql.wikipathways.org](https://sparql.wikipathways.org/)

## Figure of RDF schema

## Exercises
### Exercise 1 - Listing of subjects
The simplest SPARQL queries to explore RDF is to retrieve full lists of subjects of a particular type, which is frequently defined with the predicate `rdfs:type` or `a` which can be used interchangably. See the below example of listing all pathways.
```sparql
SELECT ?pathway 
WHERE {
?pathway a wp:Pathway .
}
```
By looking at the RDF schema figure, you should be able to adapt the SPARQL query to answer all questions that follow.

- Question 1.1: What would we need to replace `wp:Pathway` with to extract all datanodes? 
- <button onclick="toggleAnswer('q1.1')">Answer</button><span id="q1.1" style="visibility: hidden">wp:DataNode</span>
- Question 1.2: What would we need to replace `wp:Pathway` with to extract all metabolites? 
- <button onclick="toggleAnswer('q1.2')">Answer</button><span id="q1.2" style="visibility: hidden">wp:Metabolite</span>

Because the WikiPathways RDF contains many properties of all subjects (such as pathways), we can also directly request all contents through the SPARQL query. For example, to extract the pathway title, we add `?pathway dc:title ?pathwaytitle` to the SPARQL query and add `?pathwaytitle` in the `SELECT` list. The returned table upon running the query will get wider, so you might need to scroll to the right to see it all. 

- Question 1.3: What would we need to add to the query to extract the description of the pathway? 
- <button onclick="toggleAnswer('q1.3')">Answer</button><span id="q1.3" style="visibility: hidden">Adding another variable to the `SELECT` list and requesting that variable by adding in the query `?pathway dc:description ?[new variable name]`. This should return a table with the added column.</span>
- Question 1.4: What would we need to add to the query to extract the identifiers of pathways? 
- <button onclick="toggleAnswer('q1.4')">Answer</button><span id="q1.4" style="visibility: hidden">Adding another variable to the `SELECT` list and requesting that variable by adding in the query `?pathway dcterms:identifier ?[new variable name]`. This should return a table with the added column.</span>
- Question 1.5: What would we need to add to the query to extract to which organism name pathways apply to? 
- <button onclick="toggleAnswer('q1.5')">Answer</button><span id="q1.5" style="visibility: hidden">Adding another variable to the `SELECT` list and requesting that variable by adding in the query `?pathway wp:organismName ?[new variable name]`. This should return a table with the added column.</span>

### Exercise 2 - Counting of subjects
This exercise is about creating simple SPARQL queries that count particular types of subjects in the RDF. See the example SPARQL query below that counts the number of pathways in the RDF.

```sparql
SELECT (count (?pathway) as ?npathway) 
WHERE {
?pathway a wp:Pathway .
}
```

When copying this SPARQL query and executing it, you will find that the WikiPathways contains 3094 pathways.

- Question 2.1: How many GeneProducts are present in the WikiPathways RDF? 
- <button onclick="toggleAnswer('q2.1')">Answer</button><span id="q2.1" style="visibility: hidden">37146</span>
- Question 2.2: How many proteins are present in the WikiPathways RDF? 
- <button onclick="toggleAnswer('q2.2')">Answer</button><span id="q2.2" style="visibility: hidden">16145</span>


### Exercise 3 - More detailed exploration
count pathways in community
Listing human pathways
list pathways that have gene with Ensembl ID X
give matching ChEBI ID from metabolites with HMDB ID
list uniprot IDs for all nodes in pathway X
count pathways for each human pathway

### Exercise 4 - Federated SPARQL query

### End
Thank you for your participation. For any feedback or questions about this section, please contact Marvin Martens (marvin.martens@maastrichtuniversity.nl).
