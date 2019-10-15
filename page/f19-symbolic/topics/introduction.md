---
layout: post
title: Introduction
permalink: /f19-symbolic/introduction
---
<br>

> Biomedical informatics (BMI) is the interdisciplinary field that studies and pursues the **effective uses of biomedical data, information, and knowledge** for scientific inquiry, problem solving, and decision making, motivated by efforts to improve human health.
>
> -- <cite>American Medical Informatics Association (AMIA)</cite>{% include sidenote.html id="bmi_def" note="Kulikowski et al. JAMIA. 2012 Nov 1;19(6):931-8. [doi:10.1136/amiajnl-2012-001053](https://doi.org/10.1136/amiajnl-2012-001053)" %}

## Data, information, knowledge

<span class="newthought">Biomedical informatics</span> is fundamentally a field concerned with data, information, and knowledge.

Data are the building blocks of information.
Raw lab test values, clinical code occurrences, and patient gene sequences are examples of biomedical data.
Our purpose for using medical data is ultimately to extract information and gain knowledge.

Information is data with context and meaning.
In the examples given, information could be the contextualization of a number to a lab test value, a code in a diagnosis field to a disease concept, or a set of sequencing reads to a set of variant calls.
The difference between data and information is the difference between `(PID=41235934,6.7)` and, "Jane Doe HbA1c = 6.7%".

Knowledge is the highest level in this hierarchy{% include sidenote.html id="note_knowledge" note="Knowledge is the highest level with which biomedical informatics is concerned, though [wisdom is often added](https://en.wikipedia.org/wiki/DIKW_pyramid) as the fourth and highest concept in the data-information-knowledge (or data-information-knowledge-wisdom in that case) hierarchy." %}, and it is a difficult concept to define.
Unlike data or information, knowledge is a subjective, human phenomenon{% include sidenote.html id="note_knowledge2" note="Weinberger takes issue with knowledge even being represented in this hierarchy as derived from information. \"[K]nowledge is not determined by information, for it is the knowing process that first decides which information is relevant, and how it is to be used.\" ([source](https://hbr.org/2010/02/data-is-to-info-as-info-is-not))" %}.
An example of knowledge is that Dr. Roe knows that Jane's HbA1C test is [indicative of diabetes](https://medlineplus.gov/lab-tests/hemoglobin-a1c-hba1c-test/).

Knowledge enables clinicians to treat patients, and clinical knowledge can be discovered, provided, and supported by biomedical informatics.
In the study of symbolic methods, knowledge includes the relationships between concepts, the structure and types of relationships, and the relationships between concepts and their attributes{% include sidenote.html id="note_knowledge3" note="The discussion so far is meant to motivate our study, not to present the final word on these concepts. Many of the definitions given here are debatable. There is also inherent ambiguity, as one person's knowledge may be another's data." %}.

## Symbolic methods

<span class="newthought">Symbolic methods</span> use explicit representations and previously-known relationships to gain information from data{% include sidenote.html id="sym_nonsym" note="[Helpful article](https://medium.com/intuitionmachine/the-two-paths-from-natural-language-processing-to-artificial-intelligence-d5384ddbfc18) on symbolic vs nonsymbolic methods in NLP" %}.



In other words, data + information/knowledge = more information/knowledge.

Incorporating existing information/knowledge in the pursuit of further information/knowledge presents two key challenges:

1. Standardization that ensures interoperability between data sources and prevents incorrect redundancies.
2. Knowledge representation that captures relationships between concepts.

## Interoperability

>Interoperability is the ability of different information systems, devices and applications (‘systems’) to access, exchange, integrate and cooperatively use data in a coordinated manner, within and across organizational, regional and national boundaries, to provide timely and seamless portability of information and optimize the health of individuals and populations globally.
>
> -- <cite>Healthcare Information and Management Systems Society (HIMSS)</cite>{% include sidenote.html id="interop_def" note="HIMSS Dictionary of Health IT terms, acronyms, and organizations. 2017. ([link](https://www.himss.org/library/interoperability-standards/what-is-interoperability))" %}

<span class="newthought">Interoperability</span> in the context of biomedical data refers to the ability of systems to exchange data, information, and knowledge among various types of actors within and between institutions.

In essence, interoperability means that knowledge is shared among all parties either involved in the care of a patient or who are allowed to access the records{% include sidenote.html id="interop_def2" note="Note: interoperability does not refer specifically to electronic health records." %}.

Interoperability can be divided into a [hierarchy](https://www.himss.org/library/interoperability-standards/what-is-interoperability) based on the ability to exchange data, information, or knowledge{% include sidenote.html id="interop_def2" note="The 4th edition of the HIMSS Dictionary of Healthcare Information Technology Terms (2017) includes a highest level, Orgazational interoperability. In essence this level indicates that agreement has been reached about when and why data can be exchanged." %}.

Foundational interoperability deals with the exchange of _data_ at the lowest level, without requiring that the receiving system be able to interpret the data.
An example of foundational interoperability is a medical device that can send data to a medical record system, without the data being in a format that the system understands.

Structural interoperability is achieved once foundational interoperability is paired with a standardized format for _information_ exchange.
For example, two systems are structurally interoperable if they can exchange JSON documents containing patient records.
However, while both systems may use the same JSON schema, they may use different vocabularies to encode concepts.

Semantic interoperability describes when systems can use the information they exchange between one another.
In other words, two systems can share _knowledge_.
For clinical data, this means that two systems share the format (eg. data encoding, file type) and semantic encoding (eg. same terminology for drugs) of the data they exchange.

## The curly braces problem

<span class="newthought">An early approach</span> to the interoperability of medical knowledge was the Arden syntax, a language which allows clinical decision support tools to be shared across multiple health record systems{% include sidenote.html id="arden" note="Hripcsak G. Computers in Biology and Medicine. 1994 Sep 1;24(5):331-63. [doi:10.1016/0010-4825(94)90002-7](https://doi.org/10.1016/0010-4825(94)90002-7)" %}.

Because different hospitals store data differently, the syntax was designed with institution-specific mappings inside curly braces.
In order to implement a medical logic module (MLM) at a new institution, one needs only to provide references to fields as defined in the institution's database.

For example, to find the minimum serum potassium for a patient, the Arden syntax would read

```
a : = read min ( {‘serum potassium’} )
```
To implement the code, an institution must replace `{serum potassium}` with the field in their database for serum potassium.
While this sounds simple, such customizations are nontrivial and can often require expert medical knowledge to implement.
Barriers to interoperability based on interface challenges and different data standards are referred to as the "curly braces problem".
