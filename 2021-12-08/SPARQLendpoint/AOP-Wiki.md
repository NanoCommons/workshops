# Querying AOP-Wiki

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
The AOP-Wiki SPARQL endpoint is loaded with RDF of the Adverse Outcome Pathway (AOP)-Wiki database (https://aopwiki.org/). The AOP-Wiki serves as the primary repository of qualitative information for AOPs and is a central component in the AOP development effort coordinated by the Organisation for Economic Co-operation and Development (OECD). These AOPs describe mechanistic information about toxicodynamic processes and can be used to develop effective risk assessment strategies. An AOP is initiated by a stressor (e.g. a chemical) that causes a Molecular Initiating Event, which is followed by Key Eevents (measurable, essential steps) along a pathway towards an Adverse Outcome for an organism or population. KEs are connected through Key Event Relationships (KERs), which capture the evidence supporting the AOP in a structured way. 

The AOP-Wiki SPARQL endpoint is accessible on [https://aopwiki.rdf.bigcat-bioinformatics.org](https://aopwiki.rdf.bigcat-bioinformatics.org/)

## Figure of RDF schema


## Exercises
### Exercise 1 - listing of subjects
The simplest SPARQL queries to explore RDF is to retrieve full lists of subjects of a particular type, which is frequently defined with the predicate `rdfs:type` or `a` which can be used interchangably. See the below example of listing all Key Events.

```sparql
SELECT ?KE 
WHERE {
?KE a aopo:KeyEvent .
}
```

By looking at the RDF schema figure, you should be able to adapt the SPARQL query to answer all questions that follow.

- Question 1.1: What would we need to replace `aopo:KeyEvent` with to extract all Adverse Outcome Pathways? <button onclick="toggleAnswer('q1.1')">Answer</button><span id="q1.1" style="visibility: hidden">aopo:AdverseOutcomePathway</span>
- Question 1.2: What would we need to replace `aopo:KeyEvent` with to extract all Stressors? <button onclick="toggleAnswer('q1.2')">Answer</button><span id="q1.2" style="visibility: hidden">cheminf:0000000</span>

Since the Key Event links can bring you to the AOP-Wiki for further exploration of the corresponding webpage, we can also directly request all their contents through the SPARQL query. For example, to extract the Key Event title, we add `?KE dc:title ?KEtitle` to the SPARQL query. The returned table upon running the query will get wider, so you might need to scroll to the right. 

```sparql
SELECT ?KE ?KEtitle
WHERE {
?KE a aopo:KeyEvent .
?KE dc:title ?KEtitle .
}
```

- Question 1.3: What would we need to add to the query to extract the description of the Key Events? <button onclick="toggleAnswer('q1.3')">Answer</button><span id="q1.3" style="visibility: hidden">Adding another variable to the `SELECT` list and requesting that variable by adding in the query `?KE dc:description ?[new variable name]`. This should return a table with the added column.</span>
- Question 1.4: What would we need to add to the query to extract the measurement/method description of the Key Events? <button onclick="toggleAnswer('q1.4')">Answer</button><span id="q1.4" style="visibility: hidden">Adding another variable to the `SELECT` list and requesting that variable by adding in the query `?KE mmo:0000000 ?[new variable name]`. This should return a table with the added column.</span>

### Exercise 2 - counting of subjects
This first exercise is about creating simple SPARQL queries that count particular types of subjects in the RDF. See the example SPARQL query below that counts the number of Key Events in the RDF.

```sparql
SELECT (count (?KE) as ?nKE) 
WHERE {
?KE a aopo:KeyEvent .
}
```

When copying this SPARQL query and executing it, you will find that the AOP-Wiki RDF contains 1149 KE subjects.

- Question 2.1: How many Adverse Outcome Pathways are present in the AOP-Wiki RDF? <button onclick="toggleAnswer('q2.1')">Answer</button><span id="q2.1" style="visibility: hidden">333</span>
- Question 2.2: How many chemicals are present in the AOP-Wiki RDF? <button onclick="toggleAnswer('q2.2')">Answer</button><span id="q2.2" style="visibility: hidden">329</span>

Slightly more complex, can you count how many Key Events have a description?
<button onclick="toggleAnswer('')">Hint</button><span id="q4" style="visibility: hidden">Define subject as type "Key Event" and also retrieve its description. This is a forced request (not optional) so the returned table will only contain Key Events with a description</span>

<button onclick="toggleAnswer('q5')">Answer</button><span id="q5" style="visibility: hidden">389 Key Events exist that have a description.</span>

### Exercise 3 - More detailed exploration
With this exercise, the RDF will be explored a little more extensively. By combining statements in the RDF query, we can link multiple subjects and filter for content that we want to get back from the service. 

- What are the names of the which chemicals are related to stressor X
- which AOP is related to stressor X
- Which chemical is linked to AOP Y through stressor Y?

### Exercise 4 - Complete graph exploration
From AO X, which MIE?
How many AOPs have KEx as MIE
What AOs can stressor Y lead to?
