---
layout: post
title: Test-Driven Development of Ontologies
subtitle: Weekly paper discussion
categories: papers
mathjax: true
tags: [paper, DL, debugging, ontology engineering, test driven development]
---

# Summary

The paper [^fn1] introduces the idea of test-driven development from software engineering in the context of ontology engineering. The authors argue that there is no systematic testbed for ontology engineering other than manual trial-and-error approaches. Ontology engineers add, modify, or delete axioms manually and check the resulting effects by running a reasoning algorithm. The authors envision a more principled way of ontology engineering that involves the following steps:

1. Transform a competency question (CQ) into an axiom (if necessary)
2. Given: axiom \\(x\\) of type \\(X\\) to be added to the ontology
3. check the vocabulary elements of \\(x\\) are in ontology \\(O\\)
4. run TDD test twice:
    1. the first execution should fail (check \\(O \not\models x\\))
    2. update the ontology (add \\(x\\))
    3. run the test again which then should pass (check that \\(O \models x\\)) and such that there is no new inconsistency or undesirable deduction
5. Run all previous successful tests, which still have to pass (i.e., regression testing)

The authors claim that this approach to ontology engineering deepens the understanding of the ontology authoring process and the logical consequences of an axiom. Furthermore, they hypothesise that it makes roll-backs and conflicting CQs easier to manage.

# TDD Specification

The authors specify 36 generic tests that cover most of OWL 2 DL language features. For example, let \\( \alpha \\) be a class subsumption axiom of the form \\( C \sqsubseteq D\\). In order to test, whether \\(\alpha\\) is asserted or entailed by an ontology one can perform a TBox test or an ABox test:

- **TBox test**:
    * Query for all subclasses of \\(D\\)
    * If \\( C \\) is not contained in the output of the query, then the test fails
- **ABox test**:
    * Create a mock object \\(a\\) and assert \\(C(a)\\)
    * Query for all elements in \\(D\\)
    * If \\(a\\) is not contained in the output if the query, then the test fails

An experimental evaluation of TBox and ABox based TDD tests showed that TBox test are generally faster than the corresponding ABox tests. The performance difference is larger with respect to larger ontologies.

# Limitations of the Experimental Design 

The paper does not explicitly state the limitations of the performed study and does not justify all design choices.

For example:
- the experimental results are based on a rather small corpus of ontologies, namely 67
- there is no argument for the choice of the TONES repository as a test corpus
- only one SPARQL implementation (OWL-BGP) was used
- only one reasoner (HermiT 1.3.8) was used
- the results are only reported as Boxplots without further statistical analysis

# So what?

The paper succeeded to show how ontology engineering can be based on a test-driven development approach in principle. However, it does not succeed to make a convincing case for merit of such an approach in the context of ontology engineering. None of the claims made in the introduction of the paper (deepening the understanding of ontology engineering and logical consequences of an axiom, easier management of CQ conflicts, easier roll-backs) are substantiated in the rest of the paper.

I am also very sceptical about the claim that TDD facilitates the understanding of the ontology engineering process. Ontologies often contain axioms that are neither necessary nor even meaningful from a logical point of view. Redundant axioms and tautologies are often added to ontologies to ease human understanding of an ontology. However, strictly following the proposed TDD approach presented in this paper would prohibit an ontology engineer to add such axioms. This has far-reaching consequences for the maintainability and comprehension of the ontology over time. If an ontology engineer is not allowed to add more intuitive intention revealing axioms to an ontology because they are already entailed, then over time as the ontology grows, it will become increasingly harder to check whether some piece of knowledge is actually represented in the ontology in the way as intended. Furthermore, if an ontology engineers encounters a modeling error and inspects the justification for this error, he will not have access to intention revealing axioms.

Overall, I would welcome a more detailed discussion of the use cases and benefits of the proposed TDD approach for ontology engineering. While I like the idea in principle, I am not convinced by its presentation in this paper.





# References

[^fn1]: Keet, C. Maria, and Agnieszka Ławrynowicz. "Test-driven development of ontologies." International Semantic Web Conference. Springer, Cham, 2016.
