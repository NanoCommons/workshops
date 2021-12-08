[back](../README.md) 
# Querying the SPARQL endpoint of your choice

At the department of bioinformatics (BiGCaT) at Maastricht University, we host several SPARQL endpoints for biological data that exists as RDF. This workshop assumes that you already know the basics of SPARQL and RDF. For an introduction to SPARQL and RDF, please have a look at [this beginners course on SPARQL](https://bigcat-um.github.io/SPARQLTutorialBioSB2019/) first. 

Links to exercises and services of the SPARQL endpoints that BiGCaT hosts:
- [WikiPathways exercises](./WikiPathways.md) - [WikiPathways service](https://sparql.wikipathways.org/)
- [AOP-Wiki RDF exercises](./AOP-Wiki.md) - [AOP-Wiki RDF service](https://aopwiki.rdf.bigcat-bioinformatics.org/)
- [Nanosafety RDF exercises](./NanosafetyRDF.md) - [Nanosafety RDF service](https://nanosafety.rdf.bigcat-bioinformatics.org/)
- [ChEMBL RDF exercises](./ChEMBL.md) - [ChEMBL RDF service](https://chemblmirror.rdf.bigcat-bioinformatics.org/)

## Descriptions of SPARQL endpoints
### [WikiPathways](./WikiPathways.md)
WikiPathways (https://www.wikipathways.org) is a biological pathway database known for its collaborative nature and open science approaches. The road toward a sustainable, community-driven pathway database goes through integration with other resources such as Wikidata and allowing more use, curation and redistribution of WikiPathways content. The SPARQL endpoint allows the access of the WikiPathways RDF and integrate its content with other databases. The RDF contains all pathways, their datanodes (genes, proteins, metabolites, etc.), author information, molecular descriptors, and more.

### [AOP-Wiki RDF](./AOP-Wiki.md)
The AOP-Wiki SPARQL endpoint is loaded with RDF of the Adverse Outcome Pathway (AOP)-Wiki database (https://aopwiki.org/). The AOP-Wiki serves as the primary repository of qualitative information for AOPs and is a central component in the AOP development effort coordinated by the Organisation for Economic Co-operation and Development (OECD). These AOPs describe mechanistic information about toxicodynamic processes and can be used to develop effective risk assessment strategies. An AOP is initiated by a stressor (e.g. a chemical) that causes a Molecular Initiating Event, which is followed by Key Eevents (measurable, essential steps) along a pathway towards an Adverse Outcome for an organism or population. KEs are connected through Key Event Relationships (KERs), which capture the evidence supporting the AOP in a structured way.

### [Nanosafety RDF](./NanosafetyRDF.md)
Adverse Outcome Pathways (AOPs) have been proposed to explore interactions of chemicals/materials with biological systems. Each AOP starts with a molecular initiating event (MIE) and possibly ends with adverse outcome(s). So far, we do not fully understand how many nanomaterials interact with proteins, biomembranes, cells, and biological structures in general. There is limited insight into the toxicology-related key events (KEs) they trigger, such as oxidative stress and inflammation, or the biological processes underlying these KEs. For this SPARQL endpoint we integrate the annotation of nanomaterials and their MIEs with ontology annotation to demonstrate how we can then query AOPs and biological pathway information for these materials.

### [ChEMBL RDF](./ChEMBL.md)
ChEMBL is a manually curated database of bioactive molecules with drug-like properties. It brings together chemical, bioactivity and genomic data to aid the translation of genomic information into effective new drugs. Built upon the ChEMBL database, an RDF representation of the ChEMBL database is produced by the European Molecular Biology Laboratory - European Bioinformatics Institute (EMBL-EBI) and provided for [download](https://www.ebi.ac.uk/rdf/services/sparql). The ChEMBL RDF model uses a basic internal ontology, called the ChEMBL Core Ontology (CCO), to identify all of the primary entities (e.g., Documents, Assays, Substances, Targets) in the ChEMBL database. The department of Bioinformatics (BiGCaT) at Maastricht University took the initiative to host the RDF and expose it to the scientific community through a SPARQL endpoint where queries can be executed against the RDF to find answers to biological questions.


## Exercises per SPARQL endpoint
- [WikiPathways](./WikiPathways.md)
- [AOP-Wiki RDF](./AOP-Wiki.md)
- [Nanosafety RDF](./NanosafetyRDF.md)
- [ChEMBL RDF](./ChEMBL.md)


