---
layout: post
title: Lab 6
permalink: /f20-symbolic/lab6
---



## Admin

Submit a .sql file which can be run against a database in OMOP CDM format.

## Intro

<span class="newthought">One of the first</span> things to do when starting an observational study is to consider sample size.
In this lab, you'll check this for the study you designed.
I'll run these queries against actual data and report back numbers to you this week.

## Instructions

Create a SQL script to give an approximate count for the number of people you could enroll in the observational study you proposed.
You'll need to define your criteria for an OMOP database in order to accomplish this.
You may create temporary tables if needed.

## Suggestions

Basically, count how many people meet your inclusion/exclusion criteria, and how many people (approximately) had the exposure of interest.

I apologize that I don't have any simulated patients available, so you'll need to rely on the documentation of the OMOP common data model to understand the tables involved.
[The Book of OHDSI](https://ohdsi.github.io/TheBookOfOhdsi/CommonDataModel.html) and the [OMOP CDM wiki](https://github.com/OHDSI/CommonDataModel/wiki) are great resources for this.
Most likely, you'll be using `condition_occurrence`, `measurement`, `procedure_occurrence`, `person`.
[Athena](http://athena.ohdsi.org/) nicely allows you to filter by domain, which more or less corresponds to the tables.

## Example

Trivial example, but a basic idea what I'm hoping to see.

Suppose I wanted to see how many people under 18 had hypertension.

```sql
SELECT COUNT(DISTINCT person_id)
FROM concept_ancestor
INNER JOIN condition_occurrence ON descendant_concept_id = condition_concept_id
INNER JOIN person USING (person_id)
WHERE ancestor_concept_id = 316866 AND year_of_birth <= 2002
```
