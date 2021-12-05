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

## Figure of RDF schema


## Exercises

### Exercise 1 - counting of subjects
This first exercise is about creating simple SPARQL queries that count particular types of subjects in the RDF. See the example SPARQL query below that counts the number of Key Events in the RDF.

```sparql
SELECT (count (?KE) as ?nKE) 
WHERE {
?KE a aopo:KeyEvent .
}
```

When copying this SPARQL query and executing it, you will find that the AOP-Wiki RDF contains 1149 KE subjects.

Based on the RDF schema, you should be able to create SPARQL queries that count:
- Adverse Outcome Pathways - <button onclick="toggleAnswer('q1')">Answer</button><span id="q1" style="visibility: hidden">333</span>
- Chemicals - <button onclick="toggleAnswer('q2')">Answer</button><span id="q2" style="visibility: hidden">329</span>

Slightly more complex, can you count how many Key Events have a description?
<button onclick="toggleAnswer('q4')">Hint</button><span id="q4" style="visibility: hidden">Define subject as type "Key Event" and also retrieve its description.</span>

<button onclick="toggleAnswer('q5')">Answer</button><span id="q5" style="visibility: hidden">389 Key Events exist that have a description.</span>

### Exercise 2 - More detailed exploration
- which chemicals are related to stressor X
- which AOP is related to stressor X
- Which chemical is linked to AOP Y through stressor Y?

### Exercise 3 - Complete graph exploration
From AO X, which MIE?
How many AOPs have KEx as MIE
What AOs can stressor Y lead to?
