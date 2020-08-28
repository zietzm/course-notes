---
layout: post
title: SNOMED-CT
permalink: /f19-symbolic/snomed
---
<br>

> SNOMED International is a not-for-profit organization that owns, administers and develops SNOMED CT, the world’s most comprehensive clinical terminology.
>
> -- <cite>SNOMED website</cite>{% include sidenote.html id="quote" note="\"Our Organization\" ([link](https://www.snomed.org/our-organization/our-organization))" %}

<br>

<span class="newthought">SNOMED CT</span>{% include sidenote.html id="abbrev" note="SNOMED was previously an abbreviation for **S**ystematized **No**menclature of **Med**icine, though this meaning has since been removed for branding purposes." %} is a clinical reference terminology.
It is considered to be one of the best maintained and most comprehensive clinical terminology available.
SNOMED CT has rich, formal definitions, and it is in use throughout the world.

## Desiderata compliant

<span class="newthought">All of</span> Cimino's desiderata are manifest in SNOMED CT{% include sidenote.html id="desiderata" note="In fact, SNOMED CT's Editorial Guide has [an appendix](https://confluence.ihtsdotools.org/display/DOCEG/Medical+Vocabularies+-+J.+Cimino) outlining how SNOMED CT meets all of Cimino's requirements." %}.

1. SNOMED CT is the most **comprehensive** clinical terminology in the world, supporting both pre- and post-coordination.
Post-coordinated expressions greatly expand SNOMED CT's coverage and are specified using the same compositional grammar used to define pre-coordinated concepts{% include sidenote.html id="snomedpost" note="More information can be found in the subsection on post coordination within the SNOMED CT Starter Guide's [section on expressions](https://confluence.ihtsdotools.org/display/DOCSTART/7.+SNOMED+CT+Expressions)." %}.

2. SNOMED CT is a **concept-oriented** terminology.
Concept-orientation means that SNOMED CT assigns exactly one meaning per term and one term per meaning.

3. SNOMED CT maintains **concept permanence**, including identifier permanence.
Concepts can be flagged as inactive{% include sidenote.html id="active" note="\"Meaning of the Active Field\" ([link](https://confluence.ihtsdotools.org/display/DOCRELFMT/3.1.4+Meaning+of+the+Active+Field))" %} but are never removed.

4. Concepts in SNOMED CT have unique, numeric, **nonsemantic identifiers**.{% include sidenote.html id="nonsem" note="For example, the concept assigned SCTID 118600007 has as its preferred term, \"Malignant lymphoma (disorder)\"." %}

5. SNOMED CT supports **polyhierarchy**, meaning concepts can have multiple parents.{% include sidenote.html id="polyhier" note="For example, \"Malignant lymphoma (disorder)\" has two parents: \"Lymphoreticular tumor (disorder)\" and \"Malignant tumor of lymphoid, hemopoietic AND/OR related tissue (disorder)\"." %}

6. As mentioned previously, SNOMED CT has **formal concept definitions**.{% include sidenote.html id="formaldef" note="For example, \"Malignant lymphoma (disorder)\" is defined using two axioms: \"Is a (attribute)  --  Disease (disorder)\" and \"Associated morphology (attribute)  --  Malignant lymphoma - category (morphologic abnormality)\"" %}

7. SNOMED CT does not allow terms with the phrase, **"Not elsewhere classified."**

8. **Multiple granularities** are possible with SNOMED CT, thanks to its hierarchical organization and ability to navigate from less- to more-specific concepts.

9. SNOMED CT provides **multiple consistent views**{% include sidenote.html id="cons" note="Other components of this desideratum are left to software implementation, such as showing certain users only less granular concepts, etc." %}, meaning that a concept is identically represented regardless of how it was reached in the hierarchy.


10. **Context representation**---as explained by Cimino and as explored in the previous section---has two main components.
First, controlled vocabularies should include a grammar of use that restricts what types of statements are possible.
SNOMED CT has a concept model that restricts possible types of relationships between specific types of concepts.
Second, controlled vocabularies should be able to represent clinical context: for example, the circumstances in which a diagnosis was made.
SNOMED CT includes codes for many clinical circumstances under the second-level concept, "Administrative statuses (finding)"{% include sidenote.html id="context" note="For example, \"Appointment date (finding)\" or \"Patient new to provider (finding)\"" %}.

11. SNOMED CT has had a **graceful evolution**, adhering to principles of concept and identifier permanence, non-redundancy, etc.

12. SNOMED CT's rich formal definitions allow **redundant concept recognition**{% include sidenote.html id="redundant" note="For example, \"Mixed myocardial ischemia and infarction (disorder)\" is defined using both \"Is a (attribute)\"  --  \"Myocardial ischemia (disorder)\" and \"Is a (attribute)\"  --  \"Myocardial infarction (disorder)\". If these terms were not in the definition, there would be redundancy between the pre- and post-coordinated representations of the meaning." %}.

## Basic units{% include sidenote.html id="redundant" note="The building blocks and fundamental structure of SNOMED CT are specified by its \"logical model\"." %}

{% include marginfigure.html url="page/f19-symbolic/img/snomed.png" description="Diagram of SNOMED CT from the [Starter Guide](https://confluence.ihtsdotools.org/display/DOCSTART/SNOMED+CT+Starter+Guide)." %}

<span class="newthought">Concepts</span> are the basic unit in SNOMED CT.
Relationships connect concepts{% include sidenote.html id="relconcept" note="Relationships themselves are concepts, so a relationship between concepts is actually a triplet of concepts: (concept, relationship, concept)." %}, while descriptions connect concepts to additional information.

## Concepts

<span class="newthought">Concepts</span> are defined using relationships.
Each type of concept has a specified set of relationship types that are possible and that can be used for definition.

All concepts have a nonsemantic, unique, numeric identifier{% include sidenote.html id="relconcept" note="An SCTID is between 6 and 18 digits. ([source](https://confluence.ihtsdotools.org/display/DOCRELFMT/6.1+SCTID+Data+Type))" %}.

Concepts in SNOMED CT are either primitive or fully defined.
Full definition means that a concept's formal definition is unique and that any other concept meeting the definition is a subtype.
Primitive concepts are those which are not fully defined.

## Relationships

<span class="newthought">Relationships</span> connect concepts.
There are two classes of relationships in SNOMED CT: subtype and attribute.

"Is a" relationships are the subtype (or "hierarchical") relationships in SNOMED CT.
Increasingly granular concepts can be found by traversing "is a" relationships from the top level.

Attribute relationships include all other relationships.
There are 98 approved types of attributes{% include sidenote.html id="redundant" note="There are also 192 unapproved attribute types, though these are not described further here. ([More information on unapproved attributes](https://confluence.ihtsdotools.org/display/DOCTSG/10.1.4+Sanctioned+and+unsanctioned+refinement))" %}.
Attribute relationships include information like location, composition, context, numerical units, etc.
These pieces of information are still relationships, though, meaning they connect concepts to one another{% include sidenote.html id="attrib" note="One way to distinguish attribute from \"is a\" relationships is that attributes connect concepts not in the same hierarchy, meaning not connected on the same path." %}.

Attribute relationships are restricted in their application.
Each relationship type has a defined domain and range.
A relationship type's domain is the hierarchy to which it can be applied.
Its range is the hierarchy of allowed target concepts.

## Descriptions

Descriptions are textual information associated with particular concepts.
Descriptions also have unique, nonsemantic, numeric identifiers.
There are two types of descriptions in SNOMED CT: a fully specified name and synonyms.

A concept's fully specified name is a unique string giving the concept's meaning.
Synonyms are terms that can be used to refer to a concept.
The fully specified name and one synonym are marked as preferred, while other synonyms are marked as acceptable{% include sidenote.html id="languages" note="Each translation of SNOMED CT has its own descriptions, as well as labels for preferred synonyms." %}.

<!-- ## Concept model

<span class="newthought">The concept model</span> specifies the top level concepts in SNOMED CT, the ways that concepts can be defined, and the ways that concepts can relate to one another, depending on the hierarchies in which they are located.

The root concept in SNOMED CT is "SNOMED CT Concept (SNOMED RT+CTV3)".
This root has 19 children, called "top-level hierarchies"{% include sidenote.html id="meta" note="One top level hierarchy, \"SNOMED CT Model Component (metadata)\" is an ancestor of relationship and description type concepts." %}.

{% include marginfigure.html url="page/f19-symbolic/img/dom_rng.png" description="Examples of domain and range from the [Starter Guide](https://confluence.ihtsdotools.org/display/DOCSTART/SNOMED+CT+Starter+Guide)." %} -->

## Expressions

<span class="newthought">Clinical thoughts</span> are highly complex and are often more specific than available concepts.
SNOMED CT suppports extended clinical expressions using both pre- and post-coordination.

Expressions are constructed using a structured syntax.
The purpose of this structure is to make expressions machine-readable.

The SNOMED CT compositional grammar is used for both pre- and post-coordinated terms.
Ultimately the only real difference between a pre- and post-coordinated expression is that pre-coordinated expressions have a unique identifier.

---

For example, the pre-coordinated concept "laparoscopic emergency appendectomy" is defined using three relationships:

```
116680003|is a| = 80146002|appendectomy|
260870009|priority|=25876001|emergency|
425391005|using access device| = 86174004|laparoscope|
```

The same term could be represented using post-coordination as the following:

```
80146002|appendectomy|:260870009|priority|=25876001|emergency|, 425391005|using access device|=86174004|laparoscope|
```
---

## Use cases

SNOMED CT's well-maintained polyhierarchy makes it appropriate for data aggregation and analysis.
Its comprehensiveness makes it appropriate for clinical documentation, and makes it an appropriate target for concept extraction.
