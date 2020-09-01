---
layout: post
title: Lab 4
permalink: /f20-symbolic/lab4
---


## Admin

This lab has two parts.

For the first part, submit text responses and a list/table for five drugs.
For the second part, submit either a detailed table or a commented SQL query.

## Intro

<span class="newthought">The three backbone</span> vocabularies in OMOP are SNOMED CT, RxNorm, and LOINC, for conditions, drugs, and measurements, respectively.
In this lab, we'll cover basic example uses of RxNorm and LOINC.

The [FDA Adverse Event Reporting System (AERS)](https://www.fda.gov/drugs/surveillance/questions-and-answers-fdas-adverse-event-reporting-system-faers) is a system for post-marketing drug surveillance.
In essence, the goal is to identify new drug side effects, contraindications, etc. that were not identified in clinical trials.
Clinical trials are small compared to the market for drugs.
If an adverse event occurrs in 1 in 10,000 people, for example, it may not be identified in clinical trials.
Still, such an event may be relevant if millions are exposed to the drug.

## Instructions

### AERS to RxNorm

Find FDA AERS reports for all drug exposures that started on your birthday one year.{%
include sidenote.html id="bday" note="You can pick any year for which there were at least 50 cases with a drug exposure starting that day.
If your birthday doesn't satisfy this for any year, pick a different day.
E.g. if January 01, 2019 had 49 reports, try 2018, 2017, etc., and pick one with ≥ 50 cases."
%} For each of these cases, find all drugs included as exposures for the case report.

Report the following:

How many of these drugs can be mapped to RxNorm using ingredient names?
What fraction of the drugs cannot be mapped in this way?

Take five ingredients that could not be directly matched, and search for corresponding RxNorm concepts manually.
Why were you not able to map these codes using ingredient names?{%
include sidenote.html id="reasons" note="Please specify names and reasons for all five codes.
Reasons would be things like, corresponding RxNorm concepts don't exist, AERS report had typo or used an abbreviation, etc."
%}

### LOINC

Pick a condition that lab tests can help you diagnose/rule out.{% include sidenote.html id="ltest" note="For example, any of [these](https://labtestsonline.org/conditions-index)."%}
Create a measurement-based, binary, OMOP phenotype definition for this condition.
It doesn't have to be perfect, just enough to reasonably binarize cases and controls on the basis of lab measurements.
You may report this phenotype in any reasonable format.{% include sidenote.html id="eg" note="For example, a SQL query that could be run against an OMOP MEASUREMENT table, or a table of LOINC codes and cutoff values (including units)." %}

### Example

Suppose I picked [proteinuria](https://labtestsonline.org/conditions/protein-urine-proteinuria).
A reasonable answer would be to gather related LOINC codes, determine reference ranges and typical units, and create an OMOP SQL query, like the one to find cases shown below.{% include sidenote.html id="loinc_code" note="Note, `concept_code` is an OMOP field for a concept's code in its source vocabulary.
In this case, these concepts are from LOINC, so `concept_code`s are LOINC codes." %}

```sql
SELECT DISTINCT person_id
FROM MEASUREMENT
         INNER JOIN CONCEPT ON measurement_concept_id = concept_id
WHERE
   -- Dipstick urine protein test
    (concept_code = '50561-0' AND value_source_value IN ("1+", "2+", "3+"))
   OR
   -- Point-of-care protein urine test strip
    (concept_code = '5804-0' AND value_source_value IN (
        "30", "100", "300", ">300", ">=300", ">=500", ">=1000"))
   OR
   -- Random urine protein test (> 14 mg/dl)
    (concept_code = '2888-6' AND value_as_number > 14)
   OR
   -- 24 hour urine protein (> 150 mg/24hr is the listed reference)
    (concept_code = '2889-4' AND value_as_number > 150)
   OR
   -- Protein/creatinine ratio (reference is <=0.2 mg/mg or <=200 mg/g)
    (concept_code = '2890-2' AND
     (
             (unit_concept_id = 9017 AND value_as_number > 200) OR
             (unit_concept_id = 9074 AND value_as_number > 0.2)
         )
        );
```

## Suggestions

For the first part, I've created a database called `faers`, which contains FDA AERS data from Q2 2020.
You're free to use that or handle [the data](https://fis.fda.gov/extensions/FPD-QDE-FAERS/FPD-QDE-FAERS.html) yourself.
For more information about this database, see the [faers info]({{ site.baseurl }}{{ page.dir }}misc#faers).

If you use that database, you can also map directly to OMOP tables. {% include sidenote.html id="hint" note="For example, `clinical_vocabulary.CONCEPT.concept_name`, `clinical_vocabulary.CONCEPT.vocabulary_id` and `faers.drugs_20Q2.prod_ai`, `faers.therapy_dates_20Q2.start_dt` may be relevant fields for this part." %}

If you use the `CONCEPT` table, I'd suggest using `vocabulary_id LIKE 'RxNorm%'`, to include both `'RxNorm'` and `'RxNorm Extension'`.

Since, I haven't added any actual patient data to our class database, you'll have to rely on documentation for clinical data tables.
To learn about OMOP tables and fields (especially in the `MEASUREMENT` table), check out the [CDM wiki](https://github.com/OHDSI/CommonDataModel/wiki).
