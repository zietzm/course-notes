---
layout: post
title: Lab 2
permalink: /f20-symbolic/lab2
---

## Admin

There's just one part to this lab.

Please submit a table in machine-readable format (or a link to a public/shared one) on Canvas (more on this below).

## Intro


<span class="newthought">One of the</span> most common tasks encountered in observational clinical research is phenotype definition.

In short, this means taking your understanding of which patients you'd *like* to study and figuring out how to *actually find* these patients in your database.

We'll use clinical trials as proxies for observational studies we might want to perform.

## Instructions

Pick three clinical trials from <https://clinicaltrials.gov>, and manually code their inclusion/exclusion eligibility criteria using ICD-10 (CM).
{% include sidenote.html id="instr1" note="You may use fewer than three trials if one has extensive criteria, but please identify at least 30 concepts in total." %} Try to pick the broadest, most inclusive possible mappings for each concept you identify.
{% include sidenote.html id="instr11" note="You'll need some way to search for ICD codes.
There are lots of sites that let you browse ICD-10.
I typically use <https://www.icd10data.com> and <https://athena.ohdsi.org>, though Google searches like \"hypertension ICD 10\" also tend to give pretty good results.
See also: [Suggestion](#suggestion)" %}

Please submit a table in a machine-readable format using the schema in the example below.{% include sidenote.html id="sub" note="I'm not picky about the format.
Anything reasonable is acceptable: a link to a public Google sheet, a CSV/TSV file, an Excel spreadsheet, etc." %}

◼️

Here's an example of what I mean.

### Example

[NCT01810029](https://clinicaltrials.gov/ct2/show/NCT01810029) appears to be an active trial at CUIMC.{% include sidenote.html id="pick-other" note="You can't pick this one :)" %} The [eligibility criteria section](https://clinicaltrials.gov/ct2/show/NCT01810029#eligibility) gives the following:

> Inclusion Criteria:
>
> 1. Male or female
> 2. Age: No limitations
> 3. CHD documented by medical history of at least one of the following: a.acute myocardial infarction (MI) within the preceding 12 months b.coronary artery bypass surgery (CABG) c. percutaneous coronary intervention (PCI, PTCA)d. chronic stable angina
> 4. Written informed consent
>
> Exclusion Criteria:
>
> 1. noncardiac life threatening illness
> 2. Severe cognitive impairment or physical disability
> 3. History of major psychiatric disorder, i.e. psychosis, dementia, or substance abuse disorder within the past year.
> 4. Left ventricular ejection fraction less than 40%
> 5. Conditions that may be a contraindications to PET perfusion imaging with adenosine stress testing, including unstable angina or myocardial infarction in the past week, aortic stenosis, uncontrolled hypertension, uncontrolled atrial or ventricular arrhythmias, second-degree or higher atrio-ventricular block in the absence of a functioning pacemaker, baseline hypotension (systolic blood pressure < 90 mm Hg), severe obstructive lung disease or decompensated heart failure.

After finding such criteria, you should identify concepts from the text that may reasonably have corresponding ICD-10-CM codes.

In this example, I identify the following: male, female, coronary heart disease, acute myocardial infarction, coronary artery bypass surgery, percutaneous coronary intervention, chronic stable angina, non-cardiac life threatening illness, severe cognitive impairment, physical disability, major psychiatric disorder, psychosis, dementia, substance abuse disorder, left ventricular ejection fraction less than 40%, unstable angina, aortic stenosis, uncontrolled hypertension, uncontrolled atrial arrhythmia, uncontrolled ventricular arrhythmia, second-degree or higher atrio-ventricular block in the absence of a functioning pacemaker, baseline hypotension, severe obstructive lung disease, decompensated heart failure.

It's a long list!{% include sidenote.html id="instr12" note="If you pick one this long, just code two trials instead of three.
Shoot for 30 concepts total." %}

For this example, I'll just run through the first five.

Male and female are certainly concepts in clinical terminologies. {% include sidenote.html id="instr2" note="For example see [Athena: male](https://athena.ohdsi.org/search-terms/terms?query=male) and [Athena: female](https://athena.ohdsi.org/search-terms/terms?query=female)." %}
ICD, though, is a classification system for diseases.
It doesn't contain codes for male and female.

A Google search for "coronary heart disease icd 10" gave me [`I25.119`](https://www.icd10data.com/ICD10CM/Codes/I00-I99/I20-I25/I25-/I25.119): "Atherosclerotic heart disease of native coronary artery with unspecified angina pectoris".
That's a pretty specific code, and we'd like to be more inclusive when searching for patients in EHR data.
If you zoom out on the ICD-10 classification tree around this code, you'll see [`I25` and all its descendants](https://www.icd10data.com/ICD10CM/Codes/I00-I99/I20-I25/I25-).
We're interested in CHD, and all codes under `I25` look potentially relevant to me.
We'll use all of those, then.

> I25, I25.0, I25.1, I25.10, I25.11, I25.110, I25.111, I25.118, I25.119, I25.2, I25.3, I25.4, I25.41, I25.42, I25.5, I25.6, I25.7, I25.70, I25.700, I25.701, I25.708, I25.709, I25.71, I25.710, I25.711, I25.718, I25.719, I25.72, I25.720, I25.721, I25.728, I25.729, I25.73, I25.730, I25.731, I25.738, I25.739, I25.75, I25.750, I25.751, I25.758, I25.759, I25.76, I25.760, I25.761, I25.768, I25.769, I25.79, I25.790, I25.791, I25.798, I25.799, I25.8, I25.81, I25.810, I25.811, I25.812, I25.82, I25.83, I25.84, I25.89, I25.9

For acute myocardial infarction, the same method{% include sidenote.html id="ex2" note="That is, a Google search to find a code, lookup the code on icd10data.com, zoom out to see the parents and children of the code Google gave us, and identify all of those codes that could be relevant.
<https://www.icd10data.com/ICD10CM/Codes/I00-I99/I20-I25/I21->" %} gives us the following codes:

> I21, I21.0, I21.01, I21.02, I21.09, I21.1, I21.11, I21.19, I21.2, I21.21, I21.29, I21.3, I21.4, I21.9, I21.A, I21.A1, I21.A9

Coronary artery bypass surgery isn't a disease, so we wouldn't expect it to be in ICD-10.{% include sidenote.html id="pcs" note="We'd expect to find it in ICD-10-PCS, but we're focused on CM here. PCS would include children of `B202`, `B212`, `B203`, `B213`, `B223`, and `B233`."%}
However, we might be able to identify people in that category through other codes.
I'm no expert in this domain, but I think [`Z95.1`](https://www.icd10data.com/ICD10CM/Codes/Z00-Z99/Z77-Z99/Z95-/Z95.1): "Presence of aortocoronary bypass graft" seems appropriate.

Finally, please put the results in a table or spreadsheet so it's easy to look through.
We'll come back to these next time.
Anything like this would be perfect:

| NCT ID | Original phrase | Identified concept | ICD-10 codes |
| --- | --- | --- | --- |
| NCT01810029 | male | male sex | None |
| NCT01810029 | female | female sex | None |
| NCT01810029 | CHD | coronary heart disease | I25, I25.0, I25.1, I25.10, I25.11, I25.110, I25.111, I25.118, I25.119, I25.2, I25.3, I25.4, I25.41, I25.42, I25.5, I25.6, I25.7, I25.70, I25.700, I25.701, I25.708, I25.709, I25.71, I25.710, I25.711, I25.718, I25.719, I25.72, I25.720, I25.721, I25.728, I25.729, I25.73, I25.730, I25.731, I25.738, I25.739, I25.75, I25.750, I25.751, I25.758, I25.759, I25.76, I25.760, I25.761, I25.768, I25.769, I25.79, I25.790, I25.791, I25.798, I25.799, I25.8, I25.81, I25.810, I25.811, I25.812, I25.82, I25.83, I25.84, I25.89, I25.9 |
| NCT01810029 | acute myocardial infarction (MI) | acute myocardial infarction | I21, I21.0, I21.01, I21.02, I21.09, I21.1, I21.11, I21.19, I21.2, I21.21, I21.29, I21.3, I21.4, I21.9, I21.A, I21.A1, I21.A9 |
| NCT01810029 | coronary artery bypass surgery (CABG) | coronary artery bypass surgery | Z95.1 |


### Suggestion

I recognize this seems like a lot of work.

Luckily, there are some shortcuts you can use.
For example, I didn't individually copy and paste all those codes from a website.
Instead, after identifying that I'd like (e.g.) [all codes starting with `I25`](https://www.icd10data.com/ICD10CM/Codes/I00-I99/I20-I25/I25-), I used [our class database](/course-notes/f20-symbolic/labs/lab1#connect-to-the-class-database) to run

```sql
SELECT DISTINCT concept_code
FROM CONCEPT
WHERE vocabulary_id LIKE 'ICD10%' AND concept_code LIKE 'I25%'
```

As always, you're free to complete this lab using whatever data resources you'd like.
Just throwing it out there, though: learning to use the OMOP tables can be a great boon, especially for tasks like this.

Also keep in mind that not all the examples you'll encounter in this lab will follow just a single ICD code with its descendants.
Don't always accept the first code Google gives you.

If you decide to use Athena for the first part, you'll want to use the "VOCAB" filter on the left and select "ICD10" and "ICD10CM".
Also, be sure to use concept *codes*, which are from ICD, not concept *ids*, which are from OMOP.
