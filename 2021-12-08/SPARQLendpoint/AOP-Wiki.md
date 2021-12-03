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
This service is a Virtuoso SPARQL endpoint that is loaded with RDF of the Adverse Outcome Pathway (AOP)-Wiki database (https://aopwiki.org/), based on the quarterly XML dumps that are provided. The AOP-Wiki serves as the primary repository of qualitative information for AOPs and is a central component in the AOP development effort coordinated by the Organisation for Economic Co-operation and Development (OECD). The database contains AOPs which are described in terms of key events (KEs). An AOP is initiated by a stressor (e.g. a chemical) that causes a Molecular Initiating Event, which is followed by KEs (measurable, essential steps) along a pathway towards an adverse outcome for an organism or population. KEs are connected through Key Event Relationships (KERs), which capture the evidence supporting the AOP in a structured way. The AOP-Wiki website provides access to the AOP information via a web interface to look up AOPs, KEs, KERs, and stressors.

The AOP-Wiki is the main environment for the development and storage of Adverse Outcome Pathways. These Adverse Outcome Pathways describe mechanistic information about toxicodynamic processes and can be used to develop effective risk assessment strategies. However, it is challenging to automatically and systematically parse, filter, and use its contents. We explored solutions to better structure the AOP-Wiki content and to link it with chemical and biological resources. Together this allows more detailed exploration which can be automated.

We converted the complete AOP-Wiki content into Resource Description Framework. We used over twenty ontologies for the semantic annotation of property-object relations, including the ChemInformatics Ontology, Dublin Core, and the Adverse Outcome Pathway Ontology. The latter was used over 8,000 times. Furthermore, over 3,500 link-outs were added to twelve chemical databases and over 6,500 link-outs to four gene and protein databases.

SPARQL queries can be used against the Resource Description Framework to answer biological and toxicological questions, such as listing measurement methods for all Key Events leading to an Adverse Outcome of interest. The full power that the use of this new resource provides becomes apparent when combining the content with external databases using federated queries. For example, we can link genes related to Key Events with molecular pathway on WikiPathways in which they occur and find all Adverse Outcome Pathways caused by stressors that are part of a particular chemical group. Overall, the AOP-Wiki Resource Description Framework allows new ways to explore the rapidly growing Adverse Outcome Pathway knowledge and makes the integration of this database in automated workflows possible.

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
- Key Event Relationships - <button onclick="toggleAnswer('q3')">Answer</button><span id="q3" style="visibility: hidden">1382</span>

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
