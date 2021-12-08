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

## Figure of simplified RDF schema
<img src="WP RDF simple schema.png">


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
With this exercise, the RDF will be explored a little more extensively. By combining statements in the RDF query, we can link multiple subjects and filter for content that we want to get back from the service. Important: when filtering for a literal (gene label, organism, etc.) the literal should have the following format:  "text"xsd:string. For example, the next query returns the title for pathway with ID WP1560:

```sparql
SELECT ?pathwaytitle WHERE{
    ?pathway a wp:Pathway .
    ?pathway dc:title ?pathwaytitle .
    ?pathway dcterms:identifier "WP4868"^^xsd:string .
}
```

- Question 3.1: What is the title of pathway with identifier WP5087? 
- <button onclick="toggleAnswer('q3.1')">Answer</button><span id="q3.1" style="visibility: hidden">Malignant pleural mesothelioma</span>
- Question 3.2: How many human (Homo sapiens) pathways are present in the WikiPathways RDF? 
- <button onclick="toggleAnswer('q3.2')">Answer</button><span id="q3.2" style="visibility: hidden">1224</span>
- Question 3.3: Can you return the count of GeneProducts in pathway with ID WP78? 
- <button onclick="toggleAnswer('q3.3')">Answer</button><span id="q3.3" style="visibility: hidden">18</span>
- Question 3.4: Which pathways have a gene with the label "BAP1"? 
- <button onclick="toggleAnswer('q3.4')">Answer</button><span id="q3.4" style="visibility: hidden">WP4018 and WP5087</span>

Challenge: construct a query that provides the count of DataNodes for each individual human pathway
- <button onclick="toggleAnswer('c')">Answer</button><span id="c" style="visibility: hidden">Link to SPARQL query: [https://bit.ly/3lMqR3d](https://bit.ly/3lMqR3d)</span>

### Exercise 4 - Federated SPARQL query
This final exercise adds an extra level of difficulty by linking the AOP-Wiki RDF with another database through SPARQL (this is called a Federated SPARQL query). In this exercise we will explore the connection between WikiPathways and AOP-Wiki. The SPARQL query will need to contain a `SERVICE` function and the final query will have the following structure: To do this exercise, you might want to do the [AOP-Wiki SPARQL endpoint tutorial](AOP-Wiki.md) first.

```sparql
PREFIX aopo: <http://vocabularies.wikipathways.org/wp#>
SELECT [variables]
WHERE {
[query WikiPathways]
SERVICE <https://aopwiki.rdf.bigcat-bioinformatics.org/sparql> {
[query AOP-Wiki]
}}
```
- Question 4: What are the titles of Adverse Outcome Pathways in AOP-Wiki that are activated by metabolites with ChEBI IDs which are present in the pathway with identifier `WP5083` in WikiPathways? 
- <button onclick="toggleAnswer('4')">Answer</button><span id="4" style="visibility: hidden">Link to SPARQL query: [https://bit.ly/3DBRMVN](https://bit.ly/3DBRMVN)</span>

### End
Thank you for your participation. For any feedback or questions about this section, please contact Marvin Martens (marvin.martens@maastrichtuniversity.nl).
