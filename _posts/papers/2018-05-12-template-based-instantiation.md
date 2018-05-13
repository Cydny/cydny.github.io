---
layout: post
title: Template-Based Content ODP Instantiation
subtitle: Weekly paper discussion
categories: papers
tags: [paper, DL, ODP, pattern, CODP, template]
---

# Summary

The paper [^fn1] discusses two different ways to use CODPs when developing ontologies. Advantages and disadvantages of both possibilities are presented and substantiated by personal experience of the authors in the context of three ontology engineering projects (VALCRI, IMSK, E-care@home) and a preliminary study (with 5 participants) designed to test these experiences.

The two approaches for using CODPs with their purported advantages and disadvantages are:

1. **Application by extension**: first, a CODP is imported as a building block into an ontology. Second, its classes and object properties are *specialised* in the ontology by creating subclasses and subproperties respectively.

    * Advantages:
        - well-known and understood by CODP researchers
        - easy to use and implement
        - potential for ontology alignment, interoperability, and data sharing
        - imports of foundational concepts help to validate the soundness of ontology design
    * Disadvantages:
        - (transitive) imports introduce many foundational entities that do not immediately make sense in the target domain
        - extensive imports increase the cognitive complexity of the ontology
        - names of imported entities of CODPs do not always reflect their indented use adequately in the target domain ontology
        - large import closures and dependencies negatively affact CODP usability
        - imported concepts of CODPs may be incompatible with the world-view of the target ontology
        - unintuitive (as reported by individuales involved in the 3 projects listed above)

2. **Application by analogy**: entities defined in a CODP are copied and possibly renamed into the target ontology.

    * Advantages:
        - no semantics from namespaces outside the scope of the ontology are introduced
        - CODPs can be adapted to the context of the target ontology/application case
        - copying and adapting a CODP to a target domain makes it easer for non-expert ontology engineers to modify and understand the pattern
    * Disadvantages:
        - classes and object properties might be instantiated multiple times
        - more manual work which complicates maintainibility and increases the risk of inconsistencies
        - interoperability of ontologies that use the same CODPs is not guaranteed 

# Template-Based CODP Instantiation

The paper proposes a new method for using an CODP by analogy: **Template-based instantiation**. The method specifies in 4 steps how parts of a CODP can be copied into a target ontology:

1. **Adapt leaf classes**: copy leaf classes and their least common subsumer into the target ontology
2. **Adapt properties**: if the domain or range of a object or data property are classes as copied by 1., then copy the property into the target ontology. If only one of domain or range is specified for an object property, then narrow the unmatched range or domain to the least common subsumer or to the leaf class level, if no least common subsumer exists.
3. **Adapt restrictions**: copy any properties involved in class restrictions on classes as copied by 1.
4. **Merge**: merge the resulting structure with existing entities in the target module.

The authors point out that further manual work may be required.

# Lack of formal rigorousness and clarity   

While the general distinction between "application by extension" and "application by analogy" was presented in a clear manner, I have a lot of questions regarding the proposed "Template-Based instantiation".

First of all, I am puzzled about the name "Template-based instantiation". The paper does not specify precisely what is meant by the terms "template" and "instantiation". Following the intuitively motivated notion of a template in the introduction of the paper, a template is synonymous to CODP. Any entity occurring in such a CODP may be copied and renamed; thereby instantiated. This instantiation seems to be performed in step 4. **Merge**. However, it is not specified how exactly. While I do admit that I know nothing about "ontology matching" and am ignorant of an obvious *modus operandi*, it is still somewhat peculiar that no references/citations are given for the intended ontology matching techniques.

Second, I am a bit uncertain what "leaf classes" are. I am guessing that a "leaf class" is a class \\(A\\) in the CODP such that there does not exist a GCI (general concept inclusion) axiom of the form \\(A \sqsubseteq B\\) where \\(B\\) is another class in the CODP. Given this assumption, I am questioning the distinguished role "leaf classes" play in CODPs. One of the main arguments for *application by analogy* was the need for customisability of a CODP towards the context of a domain. Why does the proposed method restrict itself to "leaf classes"? (If my assumption about the meaning of leaf classes is wrong, then I would not know how to interpret the term "leaf classes" other than "any class" which would supersede the introduction of a new term.) As a consequence of my lack of understanding for the term "leaf class" I am not sure what is meant by "leaf class level" as mentioned in 2. **Adapt properites**.

# Some valid arguments
The most compelling argument in the paper is the need for customisability of CODPs by ontology engineers. While ODPs are supposed to describe a reusable successful solution to a recurrent modeling problem, it is unlikely that a ODP provides a completely accurate for all contexts. Therefore, any notion of "reuse of ODP" should account for this need of customisability.

Another interesting point is the usefulness of foundational concepts in CODPs. On the one hand, it can be argued that foundational concepts add unnecessary cognitive complexity to an ontology by introducing entities that are not immediately relevant for the domain ontology. On the other hand, foundational concepts may help to validate the soundness of a design. Furthermore, foundational concepts might be used in CODPs to provide a generic solution to a modeling problem that is easily extendable to a more specific domain.

Overall, it seems that *application by extension* and *application by analogy* provide both valuable aspects to pattern based ontology engineering. Therefore, it seems most instructive to think about a unifying method for the reuse of CODPs. Ontology engineers need to have the flexibility to reuse a CODP both by analogy and extension at will.



# References

[^fn1]: Hammar, Karl, and Valentina Presutti. "Template-based content odp instantiation." The 7th Workshop on Ontology and Semantic Web Patterns. IOS Press, 2017.
