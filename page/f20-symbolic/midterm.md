---
layout: course-page
title: Midterm solutions
permalink: /f20-symbolic/midterm
---


<!-- {% include sidenote.html id="vocab" note=""%} -->

**100 points total.**

**Note: these are example solutions. Alternatives are acceptable for most questions.**

1. **[5 points] How are symbolic methods different from non-symbolic methods?**
   1. Symbolic methods make use of existing knowledge, represented semantically in terms of conceptual units and the relationships among them. Symbolic methods reason logically about existing knowledge to produce new results. Non-symbolic methods use non-semantic representations that are not understandable to humans in intermediate steps. Non-symbolic methods use rules rather than understanding to reach a solution.
   2. For example, imagine a CDS system that recommends the next billing code. A symbolic method could rank codes based on candidate codes’ relationships with existing codes (e.g. shared ancestor concepts, cross-links, etc.). A non-symbolic method could rank codes based on historical code co-occurrence patterns or machine learning, without any understanding of the semantic relationships among codes.
2. **[5 points] What biomedical informatics tasks or activities require the use of symbolic methods? Please name at least five tasks.**
   1. Concept mapping
   2. Rule-based clinical decision support (e.g. don’t allow prescription of X with Y)
   3. Phenotype definition{% include sidenote.html id="2-3" note="Symbolic methods are required when authoritative labels are not already available. When labels are available, non-symbolic phenotype definitions are possible (e.g. predict via ML)."%}
   4. Semantic interoperability between different health record systems
   5. Semantic analysis of text (e.g. clinical notes, trials inclusion criteria, academic papers, etc.)
3. **[3 points] Give three example uses for symbolic methods in biomedicine. (Note: symbolic methods, not uses for vocabularies alone).**
   1. Concept recognition/concept normalization NLP tools like Criteria2Query
   2. Phenotype definition for multi-site OHDSI studies
   3. Smart EHR systems that allow a comparison in time of lab results from different laboratories (i.e. need symbolic methods to harmonize labs that measure the same thing but may use different codes, different units, etc.)
4. **[5 points] Explain the differences among a lexicon, a controlled vocabulary, a terminology, and an ontology. Hint: describe what knowledge is provided by each resource and what differences exist regarding knowledge representation.**
   1. A lexicon is a collection of words with information about their use. For example, the UMLS SPECIALIST Lexicon provides information information about a word's syntax: variations on its spelling, part of speech, etc.
   2. A controlled vocabulary is an organized store of knowledge (represented as words and phrases) that can be used for information retrieval.
   3. A terminology is a more general concept, meaning all the specialized words and word usages that belong to a specific field.
   4. An ontology is a representation of knowledge including terms, meanings, as well as classifications, hierarchy, and cross-links to other types of information. It is a way of combining different types of information into one representation. It is distinguished from other representations by its defining axioms and rules.
   5. Terminology is a general concept, not necessarily a formal representation. A terminology could exist only in the minds of specialists. A lexicon is concerned with individual words and the details of their use. For this reason, lexicons are particularly useful for NLP tasks. A controlled vocabulary is a formal knowledge representation for a particular domain, but it concerns itself with specific words and their relationships. An ontology is a hierarchical knowledge representation, not necessarily based on terms. For example, the Gene Ontology isn't a vocabulary because the units aren't all *words* per se, but biological entities.
5. **[5 points] Provide a comprehensive comparison between UMLS and the OMOP Common Data Model Include differences and similarities.**
   1. UMLS is a set of tools, while the OMOP CDM is a format specification for an electronic health records database.
   2. The UMLS Metathesaurus and Semantic network are comparable to concepts and their relationships in the OMOP CDM. Both are essentially a compilation of existing vocabularies. Both include relationships between concepts within and between vocabularies. Neither is a vocabulary itself. Both assign identifiers beyond the identifiers used by source vocabularies. Both include synonyms, preferred terms, etc.
   3. OMOP does not include precisely the same vocabularies as UMLS. However, some of the information from UMLS has been brought into OMOP. They use different organizational structures. UMLS uses atoms, strings, terms, and concepts. OMOP uses concepts and synonyms only. UMLS also provides a categorization beyond what source vocabularies individually provide. OMOP does not do this.
6. **[5 points] What are the meanings of the term phenotype when it is used by biomedical informaticians? Does our field use the word phenotype the same as other fields (e.g. biology)?**
   1. Our field uses the word phenotype very loosely. We mean a variety of things, including the following: a set of rules defining the clinical state of a patient using electronic health record data, the definition of a cohort of patients in clinical data, the actual clinical state of a patient, any observable patient characteristic (including those changing in time and not a result of genetics or the environment).
   2. We don't use the word the same way as other fields. Geneticists use the word phenotype to mean an observable characteristic of an organism derived from genetics and the environment. Our field could consider age a phenotype, while genetics would not. When we use the word phenotyping, we tend to mean the process of defining how to find patients with a certain characteristic in electronic health record data. Phenotyping in genetics means the process of realizing a phenotype (e.g. development from embryo to adult to realize wing shape).
7. **[5 points] What is semantic interoperability, and what are the consequences when there is no or inadequate semantic interoperability? Explain the levels of interoperability we discussed in class.**
   1.  Semantically interoperable systems are able to exchange information and knowledge between systems and across barriers such as language, time, culture, etc.
   2.  We discussed four levels of interoperability. Foundational interoperability means data can be transmitted. Structural interoperability means a standardized format for information exchange exists. Semantic interoperability means systems can communicate shared understanding. Organizational interoperability means issues relating to governance, security, speed, etc. are solved as well.
8. **[3 points] Explain the curly braces problem. Is this just a problem of the Arden syntax?**
   1. The curly braces problem is the problem that different institutions use different database schemata, naming conventions, etc. When implementing one system at a new institution, various pieces of information must be manually customized. This process requires a deep understanding both of the databases and clinical concepts involved.
   2. This problem is named after the curly braces used in the Arden syntax, but it is a much broader problem than that.
   3. For example, suppose I created a CDS system that says if an HbA1c test comes back above 6.5% it should recommend the code for diabetes. This sounds simple in practice, but how do you find HbA1c at a new site? In the Epic tables we've been using for COVID analyses, we would look for the field `2_covid_measurements_noname.ord_value` where the field `2_covid_measurements_noname.component_loinc_code IN (4548, 17856)`. Then we'd have to do `CAST(REPLACE(REPLACE(REPLACE(ord_value, "<", ""), ">", ""), "%", "") AS DECIMAL(10, 5)) >= 6.5` to remove unnecessary characters added by various lab reporting systems and normalize the character value to a number. This is not a scalable way to implement new systems that may use hundreds or thousands of different measurements, diagnoses, etc.
9.  **[5 points] It’s tempting in this class to negatively contrast ICD with SNOMED CT. Explain why this is not an entirely fair comparison. (i.e. What are the purposes of the two terminologies? What are their relative strengths and weaknesses?)**
    1.  SNOMED CT and ICD 10 are not fairly comparable because they do not attempt to accomplish the same task. They are not competing vocabularies. SNOMED CT is a controlled reference terminology, while ICD 10 is a classification system used for billing and surveillance.
    2.  SNOMED CT adheres to Cimino's desiderata. It is a consistent system that represents the relationships among types of medical entities. Concepts in SNOMED CT are defined formally. SNOMED is high quality, comprehensive, consistent, and interoperable. It doesn't include extensive pre-coordination that might be helpful in the process of billing, though post-coordination is supported.
    3.  ICD is a classification system originally developed for cause of death categorization. It uses extensive pre-coordination, informed by medical billing in the United States (ICD 10 CM in particular). ICD does not incorporate polyhierarchy, and includes varying levels of granularity. Unlike SNOMED CT, ICD only includes diseases.  ICD uses semantic identifiers, which, while not suggested by Cimino in his desiderata, can be helpful for clinicians using low-quality health record interfaces for billing.
10. **[10 points] Outline Cimino’s desiderata for controlled medical vocabularies. What motivated these considerations? Why should a vocabulary adhere to them? What are the advantages of a desiderata-compliant vocabulary compared to a non-compliant one?**
    1. Cimino describes 12 desiderata:
       1. Comprehensive content (should completely represent the domain of interest, or be able to).
       2. Concept orientation (each concept has exactly one meaning and each meaning has exactly one concept)
       3. Concept permanence (concepts are never deleted from the vocabulary)
       4. Nomsemantic concept identifiers (concept identifiers should be meaningless, because concept names may change, hierarchy may evolve differently than expected, etc.)
       5. Polyhierarchy (concepts may have multiple parents)
       6. Formal definitions (concepts are defined formally in relation to other concepts)
       7. No "not elsewhere classified" terms (these are ambiguous, cannot be formally defined, have multiple meanings, etc.)
       8. Multiple levels of granularity (include both general and highly specific terms for use in different purposes)
       9. Multiple consistent views (allow use of vocabulary for different purposes, without changing relationships themselves)
       10. Ability to represent context (allow circumstance of concept usage to be represented)
       11. Graceful evolution (knowledge changes, but changes shouldn't break the other desiderata)
       12. Recognition of redundancy (allow concepts to have multiple synonym terms; enforcing formal definitions allows redundant concepts to be recognized before they are implemented).
    2. These considerations were motivated by the proliferation of competing vocabularies a few decades ago. Each university hospital working in this field was working on different vocabularies. Individual vocabularies became extremely messy and hard to maintain as redundancies and inconsistencies were introduced. High quality terminologies enable a number of applications, and standardization allows these applications to be portable between hospitals. Noncompliant vocabularies can be useful (e.g. ICD 10), but reference terminologies that adhere to the desiderata will be more consistent, long-lasting, and portable than ones which include noncompliances (e.g. redundancies, inconsistent views, single granularity, NEC, informal definitions, fleeting concepts, etc.)
11. **[5 points] For what is FHIR used? What design principles underlie it? What are the two main formats for communications under the FHIR standard?**
    1.  FHIR is a standard for exchanging electronic health information. It is used for communicating between providers, labs, applications, patients, etc.
    2.  Unlike previous HL7 version, FHIR is based on current industry standards. It seeks to be easily implemented, rigorous, and consistent. FHIR is extremely extensible thanks to an intentionally simple specification.
    3.  Seven key FHIR design principles are reuse, composability, scalability, performance, usability, data fidelity, and implementability.
    4.  FHIR uses XML and JSON formats.
12. **[5 points] For what is the HPO used? What is the difference between HPO and OMIM?**
    1.  The Human Phenotype Ontology is an ontology representing human phenotypic abnormalities (e.g. diseases). HPO can be used for a multitude of purposes, principally the algorithmic interrogation of phenotypes and the relationships among them. For example, the HPO is used to support automated differential diagnosis systems and translational research which seeks to identify highly specific patient subtypes.
    2.  The HPO was originally developed using the OMIM database. Specifically, the original HPO was generated using OMIM "Clinical Synopsis" descriptions.
13. **[2 points] What is the difference between OWL and OBO?**
    1.  OWL is the W3C Web Ontology Language. It is a knowledge representation language for describing an ontology.
    2.  OBO refers to the Open Biological and Biomedical Ontologies. These are ontologies that represent life sciences information.
    3.  OBO is based on the principles underlying OWL. Because of this, OBO ontologies can be mapped to OWL formats without loss of information.
14. **[5 points] What is post-coordination? What are the different types of post-coordination? Please provide examples for each.**
    1.  Post-coordination is the creation of concepts using other concepts in an existing vocabulary without adding these new terms to the vocabulary itself. Expressions using multiple concepts allow complex ideas to be represented, beyond what the vocabulary contains in single concepts.
    2.  The three types of post-coordination are 1. refinement (e.g. cancer of the left kidney vs cancer of the kidney), 2. qualification (e.g. surgery vs emergency surgery; nothing different about the surgery itself, but the context is different), and 3. combination (two otherwise unrelated concepts; e.g. if my spacecraft crashed a post-coordinated combination term could be: "Unspecified spacecraft accident injuring occupant, initial encounter" (real ICD code!), "Unspecified fracture of left forearm, initial encounter for closed fracture").
15. **[2 points] Which table of the UMLS Metathesaurus would you use if you want SNOMED-CT codes for concepts? Please describe a method for this task including the knowledge resources to be used in UMLS.**
    1.  MRCONSO. I would download the UMLS Metathesaurus MRCONSO.RRF file, create a table of the concepts of interest, join this table to MRCONSO.RRF, and select the concept identifier and SAUI/SCUI columns, depending on the granularity of concepts of interest.
16. **[5 points] What kinds of relationships can the phrase “is a” represent? Can you provide an example for each relationship? What is the difference between an "is a" and a "part of" relationship? Please give an example of each.**
    1.  "Is a" can indicate both a subclass and instance relationship. For example, "Michael is a person" (instance) and "university is an institution of higher education" (subclass).
    2.  "Part of" is a subset relationship. The "Is a" relationship is not inherited in the same was as "Is a" relationships. For example, "Laptop is a computer. CPU is part of a computer," implies that a laptop has all the attributes of a computer. CPU's don't have all the attributes of a laptop.
17. **[2 points] Which of the following best represents the relationship between expressiveness and tractability (↓ indicates a decrease; ↑ indicates an increase)?**
    1.  **a.     [  ] ↓ expressiveness →  ↑ reasoning time →  ↑ tractability**
    2.  **b.     [  ] ↑ expressiveness →  ↓ reasoning time →  ↑ tractability**
    3.  **c.     [ X ] ↑ expressiveness →  ↑ reasoning time →  ↓ tractability**
        1.  Expressive capacity increases reasoning time. A simple language can be reasoned about efficiently {% include sidenote.html id="expr" note="For more information, see <https://en.wikipedia.org/wiki/Expressive_power_(computer_science)>"%}.
        2.  Increased reasoning time makes the language less tractable {% include sidenote.html id="expr" note="For more information, see [Levesque and Brachman, 1987](http://www.inf.unibz.it/~franconi/dl/course/2006/articles/BrachLev.pdf)"%}.
    4.  **d.     [  ] ↑ expressiveness →  ↑ reasoning time →  ↑  tractability**
    5.  **e.     [  ] ↓ expressiveness →  ↓ reasoning time →  ↓  tractability**
18. **[3 points] What are possible biases in disease classifications?**
    1.  Diseases vary in their frequencies. Uncommon diseases may be characterized more poorly than common diseases.
    2.  Diseases have heterogeneous manifestations. Some presentations may be more represented than others.
    3.  Diseases have various causes. Some causes may not be understood or represented.
19. **[5 points] What are possible biases in EHR documentation using clinical terminologies? What are your recommendations for minimizing such biases?**
    1.  Diseases covariance with other characteristics (e.g. demographics or comorbidities) may be overestimated, leading to dismissal of uncommon combinations (e.g. male breast cancer, certain disease among young individuals, etc.)
    2.  Terminologies may be too granular or not granular enough, depending on a clinician's understanding in the moment. This can lead to inappropriate code selection.
    3.  Interface terminologies that represent clinician understanding should be used. In particular, user input should be used here.
20. **[10 points] Why is clinical terminology so hard?**
    1.  Rector gives 10 points in his 1999 paper:
        1.  Clinical terminologies are expected to serve all purposes for all people. This is too broad.
        2.  Users have different needs than software systems. These must be reconciled.
        3.  Terminologies need to fit with clinician understanding and workflow, while being functional with software and maintaining high quality terminology standards.
        4.  Terms are confused with concepts.
        5.  Terminologies must handle clinical conventions, which are not always logical.
        6.  Formalisms for concept representations are themselves challenging.
        7.  There is no single clinical consensus. Terminologies must be customizable to local, institutional, or individual preferences.
        8.  Terminologies must interoperate with existing systems that are not ideal (e.g. ICD 10).
        9.  The terminology must be capable of correctly representing the information contained in the patient record. For example, you wouldn't want the code to mean one thing and the physician note to say another.
        10. Medicine changes; terminologies must evolve. Changes must be backwards compatible.
21. **[5 points total] Given the following ontology structure. please answer the following questions.**
    1.  **[1 point] What are the five sub-ontologies of the HPO?**
        1. Phenotypic abnormality, mode of inheritance, clinical modifier, clinical course, and frequency.
    2.  **[1 point] How was the HPO initially constructed?**
        1.  See question 12. Created using information from OMIM.
    3.  **[2 points] The following figure is a DAG. What is a DAG? What are the similarity and different features between a DAG and a Tree?**
        1.  A DAG is a directed graph without cycles. Edges have direction and you can't get from any point back to itself along one direction alone. Trees are a class of DAGs which allow each node to have only a single parent.
    4.  **[1 point] The total number of annotated diseases of each phenotype term are shown next to the terms. Assume the total number of diseases annotated in the HPO is 10000. What is the Resink similarity between the term “abnormality of the hips” and the term “dislocation”?**
        1.  The nearest common ancestor of the two is "Abnormality of the musculoskeletal system", which has 1138 concepts. -log(1138 / 10000) = 0.94 (base 10 log) or 2.17 (natural log). The base of the logarithm is unspecified, so both were accepted.
