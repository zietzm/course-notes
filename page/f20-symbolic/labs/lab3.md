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

<!-- TODO:
Instructions for reflection here.
Basically, compare the ICD codes between the two.
Are they largely the same?
How much easier was the SNOMED/OMOP approach?
Did anything not get captured this way?
 -->

Here's an example of what I mean for parts 1 and 2.

### Example

Suppose you encounter the phrase, "...".
This seems like it could be a concept, but I can't find a corresponding concept in SNOMED-CT.

To post-coordinate this concept, ...

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

For example, if I had the following SNOMED codes: ..., I'd run

```sql
...
```
