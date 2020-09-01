---
layout: course-page
title: Miscellaneous information
permalink: /f20-symbolic/misc
---

## Information about course databases

### `clinical_vocabulary`

This is essentially an OMOP database without PHI, just vocabularies.

I downloaded a number of vocabularies from Athena{% include sidenote.html id="vocab" note="Specifically, I pulled CDM 5 vocabularies having the following vocabulary codes: SNOMED, ICD9CM, ICD9Proc, CPT4, HCPCS, LOINC, NDFRT, RxNorm, NDC, Gender, Race, MedDRA, Read, ATC, VA Product, VA Class, Cohort, ICD10, Ethnicity, MeSH, ICD10CM, RxNorm , Nebraska Lexicon, OMOP Extension."%} and just inserted them into new tables.
I added a number of helpful indices, which dramatically improve the performance.

This is the main database you'll be using.

### `drugbank`

I downloaded the full [DrugBank XML database dump](https://www.drugbank.ca/releases/latest), version 5.1.7.
I used [`dbparser`](https://docs.ropensci.org/dbparser/) version 1.2.0 to automatically reformat this XML document into tables.
Most of these tables were inserted directly into the database, though a few smaller, less-important tables were omitted.

You're most likely to use this database to access natural language drug indications{% include sidenote.html id="ind" note="`drugs_pharmacology.indication`"%}, though you're free to use the wealth of other information available.

### `SIDER`

Tables were downloaded from [SIDER](http://sideeffects.embl.de/download/), version 4.1.
I did not reorder columns, but I did define names where none were present.
See [the SIDER 4.1 README](http://sideeffects.embl.de/media/download/README) for more information about the columns in these tables.
{% include sidenote.html id="sider" note="In particular, note that drug names are automatically generated in the `drug_names` table.
You may want to use names from ATC codes instead (i.e. map `SIDER.drug_atc.drug_atc_code` to `clinical_vocabulary.CONCEPT.concept_code` to access the `concept_name` field.) " %}

### `faers`

This contains some data from FDA adverse event reports from the second quarter of 2020.
I renamed only tables, not fields.
For documentation, see the [ASC_NTS.pdf](https://drive.google.com/file/d/16DgEX2TlBJV7p-5CCThWEC7hdHYF-ntf/view?usp=sharing).


## Favorite online resources

1. [Athena](https://athena.ohdsi.org/)
    - ↑ The most comprehensive front-end for OMOP vocabulary tables of which I'm aware. Functional interface. ↓ Can be a bit slow, and mappings aren't named in an obvious way. Can't collect codes like in Atlas.
    - I use this on an almost daily basis.

2. [Book of OHDSI](http://book.ohdsi.org/)
    - This thing is insanely good. It has information about OMOP, which is most relevant for this class. That's only a small fraction, though. It has detailed explanations of OHDSI tools, observational research methods, and all kinds of other things. Plus, you'll recognize many of the authors from our department.

3. [Lab tests online](https://labtestsonline.org/)
    - Amazing resource for lab tests. Great place to look for reference ranges, LOINC codes, related tests, etc.

4. [ICD10Data.com](https://www.icd10data.com/)
    - ↑ Adds helpful clinical information for ICD-10 codes. Very Google-able. Comprehensive for ICD-10.  ↓ Internal search isn't always great. Not the best interface for finding relatives of a code.

5. [DrugBank](https://www.drugbank.ca/)
    - Contains tons of information about drugs, including indications, biology/chemistry/physics data, cross-links to other data sources, etc.
    - Tends to be my go-to for looking at a new drug.

6. [OBO Foundry](http://www.obofoundry.org/)
    - Huge resource of open-source, standardized, interoperable biomedical ontologies. Includes well known resources like the Gene Ontology, ChEBI, etc.


## Personal software choices

Throughout this course, you are free to use whatever setup you prefer.
It makes no difference to me, and I want you to use what you find most comfortable.

Sometimes, though, I like to see what other people use.

For SQL, I use [DataGrip](https://www.jetbrains.com/datagrip/).
{% include marginfigure.html id="dgrip" url="page/f20-symbolic/img/datagrip.png" description="Example auto-definition" %} It has a great built-in editor.
I can very easily run queries in parallel or in a queue.
It does nice auto code reformatting, which keeps you SQL files looking clean.
It also stores the database schema and can generate table definitions, which made creating the class database insanely easy.
You can get DataGrip [free with a student account](https://www.jetbrains.com/community/education/#students).

For statistical analysis, I prefer [R](https://www.r-project.org/) + [tidyverse](https://www.tidyverse.org/).
For slightly more complex code, I like [Python](https://www.python.org/) (typically install [miniconda](https://docs.conda.io/en/latest/miniconda.html)).
For both, I'm a big fan of [Jupyter notebooks](https://jupyter.org/){% include sidenote.html id="IR" note="[IRKernel for R](https://irkernel.github.io/)" %} and [conda](https://docs.conda.io/en/latest/index.html).

I'd also highly recommend [Manubot](https://manubot.org/), which enables automated scholarly manuscripts on GitHub.
