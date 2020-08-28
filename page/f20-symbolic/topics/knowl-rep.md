---
layout: post
title: Knowledge representation
permalink: /f20-symbolic/knowledge-representation
---

<br>

<span class="newthought">In the introduction</span> to this course we defined symbolic methods as methods which use existing and explicitly represented information and knowledge to gain further information and knowledge.

In order to use existing knowledge, however, we must first find ways to represent knowledge in a meaningful and usable way.
Only after knowledge representations have been developed can semantic interoperability be achieved{% include sidenote.html id="know_rep1" note="Recall our proposition in the introduction that knowledge representation and interoperability are the two key problems in symbolic methods." %}.

## What is knowledge representation?

<span class="newthought">A knowledge representation</span> is a framework for manifesting knowledge about the world in a structured manner.
In computational fields like biomedical informatics, knowledge representations are generally usable by computers to perform reasoning tasks.

Davis, Shrobe, and Szolovits characterize knowledge representations using five distinct roles that a representation can play{% include sidenote.html id="kno_rep2" note="Davis R, Shrobe H, Szolovits P. AI magazine. 1993 Mar 15;14(1):17. ([link](https://groups.csail.mit.edu/medg/ftp/psz/k-rep.html))" %}.

1. A surrogate for the real world
2. A filter for certain aspects of the world
3. Part of an idea about what constitutes intelligent reasoning
4. A medium for efficient computation
5. A medium of human expression

## Open vs closed world assumptions

<span class="newthought">One of the first</span> philosophical challenges encountered when creating a knowledge representation is how to handle uncertainty.
In other words, do we currently have all the knowledge that we may ever want to have in our knowledge representation?

The two answers to this question are known as the open and closed world assumptions.

In the closed world assumption, all facts are known.
This means that if a theoretically possible fact is not represented, it is false by assumption.

Contrast the closed world assumption with the open world assumption, in which a fact may be true, even if it is not already known to be true.
Fundamentally, the open world assumption means we assume that our knowledge is incomplete.

In developing a biomedical knowledge representation, the choice of open or closed world assumption has real consequences.
First, in the open world paradigm, concepts don't have to be entirely distinct, and differences between concepts should be defined.
Conversely, concepts are distinct in a closed world paradigm.
Second, the open world assumption leads to more extensible and scalable knowledge representations, while the closed world assumption affords greater computational efficiency.
Third, because the closed world assumption entails a number of constraints, closed world assumption knowledge representations are more easily validated.

## Reference vs interface

<span class="newthought">How a knowledge</span> representation will be used is a practical consideration that must be taken into account when designing a representation.


Terminologies are a type of knowledge representation, and they illustrate purpose-driven design.
We split terminologies into two main types: reference terminologies and interface terminologies{% include sidenote.html id="refinf" note="Some authors include other types: aggregation terminologies, which enforce strict hierarchy and disjoint concepts and which are used for aggregating data into classes (Schulz S, et al. Studies in Health Technology and Informatics. 2017;245:940-4. [doi:10.3233/978-1-61499-830-3-940](https://doi.org/10.3233/978-1-61499-830-3-940)), or administrative terminologies for health care administration and billing (Kanter AS, et al. Studies in Health Technology and Informatics. 2008;136:27.)" %}.

Reference terminologies are concept-based, polyhierarchical, controlled medical vocabularies.
SNOMED-CT and RxNorm are examples of reference terminologies.

Interface terminologies{% include sidenote.html id="interface" note="In the context of biomedical informatics, \"interface terminology\" and \"clinical interface terminology\" are often used interchangeably." %} are less strictly defined, and exist to support the entry of clinical data into computer tools, such as electronic health records or order-entry systems.
[IMO Core](https://www.imohealth.com/imo-core/) is an example of an interface terminology.

In general, the structure, content, and constraints of knowledge representations should by informed by the purpose for which they are created.

## Pre- and post-coordination

<span class="newthought">The implementation</span> of a medical vocabulary ultimately requires content.
Unfortunately, no vocabulary can ever contain all medical concepts and relationships.
There will always be medical thoughts which cannot be fully represented using existing terms.

There are two main approaches to representing complex meanings using an incomplete vocabulary: pre-coordination and post-coordination.

In pre-coordination, medical thoughts are represented by single concepts.
To include a complex thought in the vocabulary, a new term is created that represents the thought.

Post-coordination is more flexible, allowing users to combine multiple terms to represent a complex thought.

Both approaches have advantages and disadvantages.
Pre-coordination can be simpler for users, but it requires either the anticipation of all possible term combinations or a vocabulary maintenance team that is responsive to requests for new terms.
Post-coordination is more flexible and rapidly scalable, but it can be inconvenient if users want repeatedly to enter complex thoughts that contain several terms.

There are three types of post-coordination: refinement, qualification, and combination.
Refinement increases the specificity of a concept.
Qualification adds attributes not present in the original concept.
Combination uses multiple concepts to represent a given meaning.
