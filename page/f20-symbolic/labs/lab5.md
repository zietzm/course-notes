---
layout: post
title: Lab 5
permalink: /f20-symbolic/lab5
---



## Admin

Please submit your responses/thoughts to the questions below.
Any format is fine.

Everything this week is qualitative.
There's no need to submit data, queries, code, etc.

## Intro

<span class="newthought">The next</span> five labs in this class will encompass an observational clinical study.
The goal is that you'll recognize how useful what we've covered in class so far can be.

Observational clinical studies are among our department's core focuses.
We are the coordinating center for [OHDSI](https://ohdsi.org/) (pronounced "odyssey"), a global network of researchers performing observational medical research.
OHDSI created and maintains the [OMOP Common Data Model](https://ohdsi.github.io/TheBookOfOhdsi/CommonDataModel.html) (CDM), that we'll talk more about in this class.

OMOP is basically a set of rules for how to represent health record data in a database.
It defines the tables and fields, and it has standardized vocabularies allowing all kinds of information to be represented.
Almost any hospital could, in principle, transform its data to the OMOP format.

The idea is basically this: to run studies using data from many hospitals, we have everyone transform their own data to a standard format, then we can run a single study at every hospital independently, without any protected data ever needing to change hands.
In this way, OHDSI studies are able to be among the largest conducted using health record data.

You'll run an OHDSI study in the next few labs.{% include sidenote.html id="1" note="Technically, we'll just use Columbia data, so it's not a network study."%}


## Instructions

Come up with a hypothesis for an observational biomedical study.
Pick something with a _**biological basis**_.{% include sidenote.html id="2" note="I'm requiring this so that everyone's study can incorporate material from different parts of the course. For instance, pick something like, \"Inhibition of gene x via drug y reduces risk of disease z.\" Please don't pick a hypothesis that is rooted in things other than biology (e.g. providers are more likely to do x when y is the case)."%}

Explain why the question matters and why your hypothesis is plausible.

Explain the variables involved{% include sidenote.html id="var" note="For example, if your hypothesis was, \"I think comorbidities explain COVID-19 risk more than age,\" your variables would be age and relevant comorbidities (e.g. hypertension, lung diseases, etc.), and your outcome would be severe COVID-19 outcomes (e.g. organ failure, intubation, death, etc.)."%}. What kind of relationship between independent variables and outcomes do you expect?

Scientific studies typically consider one or more controls.
Try to come up with both a positive and negative control for your outcome of interest.{% include sidenote.html id="21" note="Positive controls are known to have nonzero effect, while negative controls are known to have zero effect. They are used as checks on the methods."%}

Are there other variables that would be good comparisons as well?
For example, if you're interested in a drug's effect, you may want to compare with other drugs in the same class.

Who should be included in your study?
Come up with basic criteria for inclusion and exclusion.{% include sidenote.html id="3" note="Don't worry too much about getting it perfect. We'll talk about confounders next week. Just think about who should be in a comparison related to your hypothesis."%}

◼️

## Considerations

Consider sample sizes. Even the largest observational network studies are underpowered if only a tiny fraction of people are eligible for the study. Try to make your criteria broad enough to include people while specific enough to exclude people who shouldn't be included. Try not to pick a super rare disease or a super uncommon drug, etc. You should be able to get an intuition about this on the internet.


