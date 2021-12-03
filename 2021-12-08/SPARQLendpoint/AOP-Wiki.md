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
- Adverse Outcome Pathways - <button onclick="toggleAnswer('q2')">Answer</button><span id="q2" style="visibility: hidden">333</span>
- Chemicals - <button onclick="toggleAnswer('q2')">Answer</button><span id="q2" style="visibility: hidden">329</span>
- Key Event Relationships - <button onclick="toggleAnswer('q2')">Answer</button><span id="q2" style="visibility: hidden">1382</span>

Slightly more complex, can you count how many Key Events have a description?
<button onclick="toggleAnswer('q2')">Hint</button><span id="q2" style="visibility: hidden">Define subject as type "Key Event" and also retrieve its description.</span>

<button onclick="toggleAnswer('q2')">Answer</button><span id="q2" style="visibility: hidden">389 Key Events exist that have a description.</span>


