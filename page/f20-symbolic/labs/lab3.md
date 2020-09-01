---
layout: post
title: Lab 3
permalink: /f20-symbolic/lab3
---

## Admin

This lab has three parts.

The first is basically a redo of last week's assignment.
The second is a simple database operation.{% include sidenote.html id="reality" note="Or a grueling, hours-long click-and-wait ordeal. [I suggest](#suggestions) database :)" %} The third is a reflection.

Submit both a machine-readable table (same format guidelines as last time) and a PDF containing your responses.

## Intro

<span class="newthought">A minor theme</span> of this course is that SNOMED-CT can be an amazing entry-point to clinical data.
Many, if not most OMOP standard condition concepts are SNOMED-CT concepts.{% include sidenote.html id="book" note="See the [Book of OHDSI, Chapter 5](https://ohdsi.github.io/TheBookOfOhdsi/StandardizedVocabularies.html)" %}

I hope this lab will convince you that SNOMED-CT suits that role beautifully.

You'll redo the exercise from last time, except using SNOMED-CT instead of ICD-10 CM.{% include sidenote.html id="icd" note="While it might seem like this class spends a lot of time disliking ICD, that's an incorrect perception.
ICD is a very suitable choice for *certain* tasks." %}

The goal is that you'll appreciate why SNOMED-CT and SNOMED-CT to ICD-10 mappings are much better choices for this task than ICD-10 alone.

## Instructions

Using the same clinical trials that you chose in the previous lab, code the inclusion/exclusion eligibility criteria using SNOMED-CT. {% include sidenote.html id="snomed" note="As before, you have lots of options for data browsers.
My go-tos are [Athena](https://athena.ohdsi.org) and the [official SNOMED-CT browser](https://browser.ihtsdotools.org).
Feel free to our class database also." %}

Unlike in the previous lab, if you're not able to find an appropriate term, you should use post-coordination to create the term.{% include sidenote.html id="post" note="See the [SNOMED-CT documentation on post-coordination](https://confluence.ihtsdotools.org/display/DOCSTART/7.+SNOMED+CT+Expressions) for more information." %} Please find at least one concept that you have to create this way, even if you just pull one from some other trial.

For the second part, convert your codings into ICD-10.
In your submitted table, just add columns for both SNOMED-CT and ICD-10.{% include sidenote.html id="cols" note="Quick recap: the columns should basically be NCT ID, original phrase, concept you think it means, SNOMED-CT coding, ICD-10 coding." %}

Finally, compare the resulting ICD-10 codes between your manual mapping and the SNOMED → ICD mapped codes.
Did you find similar codes using different methods?
If not, how did the sets of codes differ?
Did you find it easier to find codes manually for ICD-10 or SNOMED-CT?
Were there any obvious omissions for either method vs the other?

Can you put into words why one might prefer the SNOMED → ICD approach over direct ICD?

◼️

Here's an example of what I mean for parts 1 and 2.

### Example

Suppose you encounter the phrase, "cancer in left kidney".
This seems like it could be a concept, but I can't find a corresponding concept in SNOMED-CT.

To post-coordinate this concept using the [SNOMED expression syntax](https://confluence.ihtsdotools.org/display/DOCSTART/7.+SNOMED+CT+Expressions), you could write:

```363518003 | Malignant tumor of kidney (disorder) | : 363698007 | Finding site (attribute) | = 18639004 | Left kidney structure (body structure) |```{% include sidenote.html id="postcoord" note="The official SNOMED browser gives expressions for pre-coordinated terms.
These tend to be pretty complex.
It's not critical that you have a perfect understanding of SNOMED expression syntax, just a basic ability and appreciation for the kinds of concepts for which post-coordination could be applied."%}

An acceptable mapping for this concept would be `C64.2`: Malignant neoplasm of left kidney, except renal pelvis.


## Suggestions

SNOMED-CT tends to be a bit less searchable on Google than ICD-10.
If you decide to use [Athena](https://athena.ohdsi.org) for the first part, you'll want to use the "VOCAB" filter on the left and select "SNOMED".
{% include sidenote.html id="codes" note="As before, you'll want to use concept *codes* (from SNOMED-CT), not concept *ids*, which are from OMOP." %} The [official SNOMED browser](https://browser.ihtsdotools.org) is also great.

For the first part of this lab, I'd suggest basically the same strategy as in the previous lab.

The second part of this lab can be either very easy or very hard, depending on what method you use.

One way to find SNOMED-CT to ICD-10 mappings is to go on Athena, find the SNOMED-CT concept, look at "Standard to Non-standard map (OMOP)", click on concepts where the vocabulary column is ICD10 or ICD10CM, and copy the concept code.

Needless to say, this would be extremely time-consuming.

Personally, I'd use standard-to-non-standard mappings from OMOP that are available in our class database.
Specifically, I'd gather the SNOMED codes for concepts I want to map and just join OMOP tables. {% include sidenote.html id="reality" note="The way I *actually* do this is by creating a table with concept name and SNOMED code, then join that on these tables.
Unfortunately, I'm not willing to open table write permissions on this database.
We only have a couple more GB on the AWS free tier, and if more were written, it'd be my credit card getting charged :(" %}

For example, if I had the following SNOMED codes: 59621000, 53741008, and 73211009, then I'd run something like this.

```sql
SELECT DISTINCT concept_A.concept_code, concept_B.concept_code
FROM CONCEPT AS concept_A
         INNER JOIN CONCEPT_RELATIONSHIP ON concept_A.concept_id = concept_id_1
         INNER JOIN CONCEPT AS concept_B ON concept_B.concept_id = concept_id_2
WHERE concept_A.concept_code IN (59621000, 53741008, 73211009)
  AND relationship_id = 'Mapped from'
  AND concept_B.vocabulary_id LIKE 'ICD10%';
```

This returns:

| concept\_code | concept\_code |
| :--- | :--- |
| 53741008 | I25.1 |
| 53741008 | I25.0 |
| 73211009 | E13.69 |
| 73211009 | E13 |
| 73211009 | E13.65 |
| 73211009 | E13.610 |
| 73211009 | E13.630 |
| 73211009 | E13.618 |
| 73211009 | E14 |
| 73211009 | E13.638 |
| 73211009 | E13.621 |
| 73211009 | E13.10 |
| 73211009 | E13.00 |
| 73211009 | E13.622 |
| 73211009 | E13.649 |
| 73211009 | E13.8 |
| 73211009 | E13.64 |
| 73211009 | E13.63 |
| 73211009 | E13.61 |
| 73211009 | E13.6 |
| 73211009 | E13.1 |
| 73211009 | E13.0 |
| 59621000 | I10 |

You should then check this mapping using `concept_name` for the mapped codes.
