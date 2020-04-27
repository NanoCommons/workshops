# Spreadsheet Annotation

[toc](./README.md) | [next](SpreadsheetAnnotation2.md)

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

---

## A Demo Spreadsheet

In this first hackathon we start by looking at a simple spreadsheet with some minimal information. Actually,
it is data from a recent publication by Labouta *et al.*, where the authors made their data collection available under an Open license:

![Demo spreadsheet](demo_spreadsheet.png)

This spreadsheet shows a number of concepts and experimental data. We see nanomaterials, physicochemical properties,
and a bit of biological assay data. We see that columns can be annotated ("all data in this column is particle sizes")
and we note that cell values may need annotation (such as the cell lines).

The data is available in two formats:

* [Tab-Separated Values](demo_spreadsheet.tsv)
* [Microsoft Excel](demo_spreadsheet.xlsx)

### Exercise 1: Browsing the eNanoMapper ontology with BioPortal

The purpose of this exercise is to see how BioPortal visualizes the eNanoMapper ontology.
A [detailed tutorial](https://enanomapper.github.io/tutorials/BrowseOntology/Tutorial%20browsing%20eNM%20ontology.html)
has been developed before.

Your task is to find the ontology term for JRCNM01000a, one of the
JRC representative industrial nanomaterials (see [[0](https://doi.org/10.1016/J.YRTPH.2016.08.008)]).

* Step 1: Visit [http://bioportal.bioontology.org/ontologies/ENM/](http://bioportal.bioontology.org/ontologies/ENM/)
* Step 2: Open the Classes tab
* Step 3: Search `JRCNM01000a`

#### Questions

1. What is the ontology term IRI for JRCNM01000a? <button onclick="toggleAnswer('q1')">Answer</button><span id="q1" style="visibility: hidden"> http://purl.enanomapper.org/onto/ENM_9000074</span>
2. What is the ontology super class of this term? And the IRI of that?<button onclick="toggleAnswer('q2')">Answer</button><span id="q2" style="visibility: hidden"> titanium oxide nanoparticle, http://purl.bioontology.org/ontology/npo#NPO_1486</span>

## Annotating the columns

When we look at the column headers, we see the following concepts:

* label (name)
* particle size
* zeta potential (experimental?)
* cell line
* exposure time
* cell viability
* journal article

In this part of the workshop, the annotation will result in written documentation: you just write down
which ontologies term match which cells in the spreadsheet.

### Exercise 2: Use BioPortal to find matching ontology terms

In this excercise your task is to find the ontology term for the concepts of the columns.
It is suggested to first search in the eNanoMapper (ENM) ontology. If you cannot find a hit,
go to the BioPortal front page and search in all ontologies.

* Step 1: Visit [http://bioportal.bioontology.org/ontologies/ENM/](http://bioportal.bioontology.org/ontologies/ENM/)
* Step 2: Open the Classes tab
* Step 3: Search for the concept represented by the column

#### Questions

Here are some examples searches and matches:

1. What is the ontology term IRI for `label`? <button onclick="toggleAnswer('q3')">Answer</button><span id="q3" style="visibility: hidden"> It is not http://purl.obolibrary.org/obo/CHEBI_35209, which is reserved to chemical groups that are used as tracer, such as fluorescent groups. 'Name' is in the eNanoMapper ontology with IRI 	
http://ncicb.nci.nih.gov/xml/owl/EVS/Thesaurus.owl#C42614 and that is a good fit. Arguable, 'molecular entity name' is a better match, as it has more semantic meaning.</span>
2. What is the ontology term IRI for `size`? <button onclick="toggleAnswer('q4')">Answer</button><span id="q4" style="visibility: hidden"> Particle size is http://purl.bioontology.org/ontology/npo#NPO_1694 but one should wonder what kind of particle size was meant here? How was it measured? What is the shape of the particle?</span>
3. What is the ontology term IRI for `article`? <button onclick="toggleAnswer('q5')">Answer</button><span id="q5" style="visibility: hidden"> First, the label is slightlt misleading. The values in this column are not articles, but they are Digital Object Identifiers (DOIs). The closest match in ENM is 'descriptor': http://purl.enanomapper.org/onto/ENM_8000019 but the OBI has a specific term for DOi with IRI http://purl.obolibrary.org/obo/OBI_0002110 (found via the BioPortal front page search).</span>

## Annotating the values

Besides the columns themselves, we also noted that two columns have values which we may want to annotation.
We see that the label and cell columns have values which we can find in ontologies too. The eNanoMapper and
NanoParticle Ontologies will have terms for the nanomaterials, whereas the eNanoMapper ontology also has
terms for the cell lines.

### Exercise 3: Use BioPortal to find matching ontology terms

The procedure is the same as before.

#### Questions

1. What is the ontology term IRI for CeO2? <button onclick="toggleAnswer('q10')">Answer</button><span id="q10" style="visibility: hidden"> http://purl.enanomapper.org/onto/ENM_9000006</span>
2. What is the ontology term IRI for Se? <button onclick="toggleAnswer('q11')">Answer</button><span id="q11" style="visibility: hidden"> http://purl.enanomapper.org/onto/ENM_9000244</span>
3. What is the ontology term IRI for PC3? <button onclick="toggleAnswer('q12')">Answer</button><span id="q12" style="visibility: hidden"> http://www.ebi.ac.uk/efo/EFO_0002074</span>
4. What is the ontology term IRI for L929? <button onclick="toggleAnswer('q13')">Answer</button><span id="q13" style="visibility: hidden"> The current eNanoMapper ontology does not have this cell line, but the Cell Line Ontology does: http://purl.obolibrary.org/obo/CLO_0007219 You can find this term by searching for L929 on the BioPortal front page.</span>

## Annotating the value units

Finally, the spreadsheet also lists a few units (mV, nm, h). It is left to the participant to look these up
in ontologies. Here, the [Units of Measurement Ontology](http://bioportal.bioontology.org/ontologies/UO/)
(UO) might be useful.

## References

* Labouta HI, Asgarian N, Rinker K, Cramb DT. Meta-Analysis of Nanoparticle Cytotoxicity via Data-Mining the Literature. ACS Nano. 2019 Jan 31; doi:[10.1021/acsnano.8b07562](https://doi.org/10.1021/acsnano.8b07562) ([Scholia](https://tools.wmflabs.org/scholia/work/Q69534939))

---

[toc](./README.md) | [next](SpreadsheetAnnotation2.md)

Copyright 2019-2020 (C) Egon Willighagen - CC-BY Int. 4.0
