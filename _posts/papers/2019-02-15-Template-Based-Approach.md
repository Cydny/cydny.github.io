---
layout: post
title: A Template-Based Approach Toward Acquisition of Logical Sentences
subtitle: Personal notes
categories: papers
mathjax: true
tags: [paper, DL, pattern, template]
---

# Summary

The paper [^fn1] discusses the potential of tool support for ontology engineering by providing templates that allow users to compose axioms by 'filling-in-the-blanks'. The authors claim that a small number of templates can account for the majority of axioms in clinical ontologies. Instead of defining a sophisticated relationships between different templates, the authors try to strike a balance between a small number of templates on the one hand, and templates that are not too general to be incomprehensible on the other hand.

# Templates

A *pattern* is characterised by axioms whose structure is repeatedly used; meaning they such axioms are identical except for specific non-logical symbols. Such a pattern is then generalised into a *template* in which the varying names are replaced by variables.

Templates are described by
* a natural language sentence indicating variable elements with underscores,
* a sample usage sentence in natural language,
* description of variations that capture different patterns,
* relationships to be captured with the template,
* the axiomatic structure of the template, i.e. a pattern with variables,

# Variations in Templates

Small variations between different patterns may be captured by the same template by allowing the logical structure of axioms to be variables as well. The instantiation process might be restricted to a fixed number of options though.

# Properties of Templates

The authors believe that organising templates into an inheritance hierarchy is not feasible. However, there characterise properties of _thoughts_ that templates may express. Examples of such thoughts are:

* the instantiation of one variable depends (or is even determined by) on another
* multiple constraints between instantiation of variable options 
* comparisons between variable elements

# Interesting Observations

The authors did not examine axioms associated with upper level ontologies. They reason that such axioms seldom produce context-independent reusable patterns due to their complexity and specificity. This is somewhat surprising since upper level ontologies are though to describe fairly general terms that are relevant across different domains. Moreover, a fair number of Ontology Design Patterns have been generated on this assumption and are considered as *directly reusable* building blocks.
 
[^fn1]: Chih-Sheng Johnson Hou, Natalya Fridman Noy, and Mark A. Musen. 2002. A Template-Based Approach Toward Acquisition of Logical Sentences. In Proceedings of the IFIP 17th World Computer Congress - TC12 Stream on Intelligent Information Processing, Mark A. Musen, Bernd Neumann, and Rudi Studer (Eds.). Kluwer, B.V., Deventer, The Netherlands, The Netherlands, 77-89.
