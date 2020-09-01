---
layout: post-19
title: Desiderata for medical vocabularies
permalink: /f19-symbolic/desiderata
---

## Motivation

{% include marginfigure.html id="nb1" url="page/f19-symbolic/img/unreadable_note.jpg" description="Example of unreadable pharmaceutical prescription ([source](https://www.reddit.com/r/pharmacy/comments/2z33vh/maybe_im_a_little_out_of_the_retail_game_but_if/?utm_source=share&utm_medium=web2x))" %}

<span class="newthought">Computers began</span> to be adopted in medical practices with the goals of increasing effectiveness, efficiency, and safety.
The idea was that clinical practice would use computer messages rather than unreadable handwriting on paper.

The need for controlled medical vocabularies became obvious with the need to standardize a huge number of computer-based clinical systems.

For example, electronic systems would contain a standardized representation of all prescribable drugs so that physicians and pharmacists could exchange prescriptions consistently and without ambiguity.

The necessity of controlled vocabularies resulted in a number of academic hospitals creating their own vocabularies.
Over time, many of these site-specific vocabularies became bloated, full of redundancies and inconsistencies.

Medical vocabularies needed high quality standards.

## The desiderata

<span class="newthought">To remedy</span> the limitations of previous work and allow interoperability, high-quality and well-maintained standardized vocabularies were needed.
In 1998, Dr. James Cimino published a paper describing 12 desirable characteristics of controlled medical vocabularies{% include sidenote.html id="desid" note="Cimino JJ. Methods of Information in Medicine. 1998;37(04/05):394-403. [doi:10.1055/s-0038-1634558](https://doi.org/10.1055/s-0038-1634558)" %}.
His requirements were intended to guide developers and have been realized in a number of standardization projects.

1. Comprehensive content
2. Concept orientation
3. Concept permanence
4. Nonsemantic concept identifiers
5. Polyhierarchy
6. Formal definitions
7. No catch-all concepts like "Not elsewhere classified"
8. Multiple levels of granularity
9. Multiple consistent views
10. Ability to represent context
11. Graceful evolution
12. Recognition of redundancy

Each of these points is covered individually below.

## Comprehensive content

<span class="newthought">One of the</span> challenges in creating medical vocabularies is to comprehensively cover the domain of interest.
Several approaches to this challenge are possible.

First, a vocabulary could add terms when needed.
This requires that users be able to suggest new terms and developers respond to suggestions.

Second, a vocabulary could create all possible terms in advance.
In medical vocabularies, this would mean, for example, creating all variants of all possible disease as terms in the vocabulary.

Third, a small number of necessary terms could be provided which users piece together to represent a meaning.
This approach is known as post-coordination{% include sidenote.html id="prepost" note="Post-coordination can be contrasted with pre-coordination, the inclusion of higher-level concepts in a vocabulary. The first and second approaches mentioned here are examples of pre-coordination." %}.

Regardless of which approach is taken, a high-quality controlled medical vocabulary should be as comprehensive as possible and use a defined method for adding missing terms.

## Concept orientation

<span class="newthought">Concept orientation</span> means that items in the vocabulary correspond to a particular meaning.

Specifically, each concept corresponds to exactly one meaning and each meaning corresponds to no more than one concept{% include sidenote.html id="desid2" note="A vague term does not correspond to a meaning. An ambiguous term corresponds to multiple meanings. A redundancy means one meaning corresponds to multiple terms. Concept orientation means a vocabulary has neither vague, ambiguous, nor redundant terms." %}.

## Concept permanence

{% include marginfigure.html id="permanence" url="page/f19-symbolic/img/permanence.png" description="As an example, the term Non-A, Non-B Hepatitis is not in current medical use. However, Hepatitis C is not equivalent to the archaic term. Some patients previously coded with the archaic term have Hepatitis C, so it is a child concept of the archaic concept. <br>(Image: Cimino JJ. Symbolic Methods slides. Lecture given 2019-09-17.)" %}

<span class="newthought">Once created,</span> concepts should never be deleted.
Unnecessary concepts can be indicated as such, but a concept's meaning cannot change.
Concept permanence is important so that previous knowledge can be interpreted unambiguously.

## Nonsemantic concept identifiers

<span class="newthought">Every concept</span> in a vocabulary should have a unique identifier.

Concepts, as such, are not equivalent to specific words or phrases.
The words or phrases used to refer to a concept can change while the concept's meaning does not.
Therefore, a concept's name should not be chosen as its identifier.

Identifiers that take into account the hierarchical relationships between concepts should also not be used, for several reasons.
First, hierarchical identifiers are unnecessary as the identifiers for concepts need not be exposed to users.
Second, assigning identifiers in a strictly hierarchical fashion is impossible when concepts can have multiple parents{% include sidenote.html id="desid2" note="Polyhierarchy means that concepts can have multiple parents. This is described further in desideratum 5, polyhierarchy." %}.
Third, fixed-length hierarchical identifiers can be insufficient if a concept has a large number of direct children.
Fourth, knowledge is dynamic, and a hierarchical identification system could be broken by reclassifying concepts, even if each concept has only a single parent.

## Polyhierarchy

{% include marginfigure.html id="polyhierarchy" url="page/f19-symbolic/img/polyhierarchy.png" description="Example of a disease polyhierarchy. <br>(Image: Cimino JJ. Symbolic Methods slides. Lecture given 2019-09-17.)" %}

<span class="newthought">Medical concepts</span> are inherently ill-suited for classification using a strict hierarchy.
Many concepts could equally well be classified into multiple, distinct categories.
Rather than having redundant concepts as children of separate parents, a polyhierarchy allows a single concept to have multiple parents.

Polyhierarchy accurately captures the richness of medical knowledge in a way that would be impossible in a strict hierarchy without redundant concepts.

## Formal definitions

<span class="newthought">Formal definitions</span> are structured concept definitions in relation to other concepts in a vocabulary.
Cimino gives the following example of a formal disease definition:

> “Pneumococcal Pneumonia” can be defined with a hierarchical (“is a”) link to the concept “Pneumonia” and a “caused by” link to the concept “Streptococcus pneumoniae”.

With formal definitions implemented, the relationships among concepts in a controlled vocabulary can be divided into definitional and assertional relationships.
Cimino gives the following example to illustrate the difference between definitional and assertional relationships:

> [L]inking “Pneumococcal Pneumonia”, via the “caused by” relationship, to “Streptococcus pneumoniae” is definitional, while linking it, via a “treated with” relationship, to “Penicillin” would be assertional.

## Reject "Not elsewhere classified"

<span class="newthought">Concepts including</span> "not elsewhere classified" ("NEC") should not be included in high-quality controlled medical vocabularies.
Such concepts cannot have formal definitions except as the negation of other concepts.

The inherent ambiguity of NEC terms means that their presence makes adding new terms very inelegant.
This conflicts with desideratum 11, graceful evolution.

{% include marginfigure.html id="graceful" url="page/f19-symbolic/img/graceful.png" description="Example of NEC terms making term addition inelegant. When somatization disorder is added, a new NEC term becomes necessary. <br>(Image: Cimino JJ. Symbolic Methods slides. Lecture given 2019-09-17.)" %}

NEC terms correspond to a number of different meanings.
To add new concepts that correspond to meanings subsumed in an NEC term, concept permanence requires that one make the new concept a child of the NEC term.
However, to retain consistency, then, a new NEC term should be added a sibling of the added term.
This process does not have any logical stopping criteria, so the careful use of NEC terms would create endless branches with new NEC terms and single sub-categorizations.

## Multiple levels of granularity

<span class="newthought">Medical vocabularies</span> are used by many people for different purposes.
A multipurpose vocabulary should have levels of granularity that are appropriate for multiple tasks.

A high degree of specificity may be required for highly specialized tasks, while such granularity might be cumbersome for a more general task.
A reusable vocabulary that supports multiple tasks should therefore have multiple levels of granularity.

Consistent granularity is also important.
For example, if multiple paths lead to a concept, then these paths should be of equal length.

## Multiple consistent views

<span class="newthought">Multipurpose</span> medical vocabularies should support multiple levels of granularity by providing purpose-specific views.

For example, if a medical record system allows providers to enter diagnoses using a vocabulary, it may be desirable to restrict the visible concepts or relationships.

{% include marginfigure.html id="consistent" url="page/f19-symbolic/img/consistent.png" description="Example of consistent and inconsistent views. On the left, concept E has the same children after being artificially split into redundant concepts. On the right, E has different children, resulting in an inconsistent view. (Image: Cimino JJ. Methods of Information in Medicine. 1998;37(04/05):394-403. [doi:10.1055/s-0038-1634558](https://doi.org/10.1055/s-0038-1634558))" %}

Additionally, if a polyhierarchy is artificially split for viewing in different contexts, the resulting redundant concepts must be identical.

## Ability to represent context

<span class="newthought">Cimino proposes</span> that a fully contextualized medical vocabulary needs to represent three types of knowledge: definitional, assertional, and contextual{% include sidenote.html id="context" note="We discussed definitional knowledge and assertional knowledge under desideratum 6, formal definitions." %}.

Contextual knowledge refers to the circumstances in which terms appear or come to appear.
For example, a single diagnosis code in a patient record alone lacks context.
Information about when a diagnosis was recorded, such as an episode of care within a patient encounter makes the information more comprehensive.

One way to implement contextualization is by adding new, circumstance-describing terms to the vocabulary itself.

Another reason for including context is to restrict the possible uses of a vocabulary.
Certain types of terms should only have certain types relationships, which should only connect to certain types of other terms.
This kind of restriction introduces a grammar of usage, which is very helpful for a comprehensive vocabulary.

## Graceful evolution

<span class="newthought">Medical knowledge evolves.</span>
Even a vocabulary that perfectly conforms to all the previous desiderata can only represent current medical knowledge.

Designers and maintainers should be conscientious about updating their vocabularies.
Change must take place, at least as knowledge progresses, but changes should be purposeful{% include sidenote.html id="evol" note="Cimino gives examples of good and bad reasons for changing a vocabulary. Good: \"[S]imple addition, refinement, precoordination, disambiguation, obsolescence, discovered redundancy, and minor name changes.\" Bad: \"[Adding] redundancy, major name changes, code reuse, and changed codes\"" %} and well-documented.

Ideas we previously discussed are also relevant here.
Changes made to a vocabulary should maintain conformance to principles like concept permanence, nonredundancy, nonambiguity, nonvagueness.

In short, graceful evolution means that changes shouldn't violate the other desidera.

## Recognition of redundancy

<span class="newthought">Redundancy is</span> when multiple concepts correspond to the same meaning{% include sidenote.html id="syn" note="Concepts must not overlap. But concepts can have attributes such as synonyms, translations, and abbreviations. Synonyms are very helpful, but they should map to non-redundant concepts." %}.
While it may seem like redundancy could be avoided by being very careful when creating new terms, redundancy can be an inevitable consequence of evolution.

Pre-coordinated concepts are higher-level entities included in a vocabulary.
A responsive development team may wish to add pre-coordinated terms that capture the most commonly-used post-coordinations.
Alternatively, pre-coordinated terms might be created as medical knowledge evolves.

Regardless of the reason for introducing new pre-coordinated concepts, they can easily introduce redundancy{% include sidenote.html id="redund" note="Cimino gives the following example: users post-coordinate left lower lobe pneumonia using separate terms for \"pneumonia\" and \"left lower lobe\".
Later, \"left lower lobe pneumonia\" is added as a new concept.
This creates a redundancy, as users could select either the new pre-coordinated term or could post-coordinate the meaning as previously." %}.

Formal concept definitions allow introduced redundancies to be recognized.
For example, a newly-introduced pre-coordinated term should be defined using the concepts used to represent it using post-coordination.
