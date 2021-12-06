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

## Figure of RDF schema

## Exercises

### Exercise 1 - Listing of subjects
Listing pathways
Listing human pathways
Listing proteins


### Exercise 2 - Counting of subjects
count pathways
count geneproducts
count metabolites
count human pathways
count pathways in community
count pathways for each human pathway
count literature references for each human pathway

### Exercise 3 - More detailed exploration
list pathways that have gene with Ensembl ID X
give matching ChEBI ID from metabolites with HMDB ID
list uniprot IDs for all nodes in pathway X

### Exercise 4 - Federated SPARQL query

### End
Thank you for your participation. For any feedback or questions about this section, please contact Marvin Martens (marvin.martens@maastrichtuniversity.nl).
