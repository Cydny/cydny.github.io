---
layout: post
title: Debugging Missing is-a structure within taxonomies
subtitle: Weekly paper discussion
categories: papers
mathjax: true
tags: [paper, DL, debugging, alignment]
---

# Summary

The paper [^fn1] discusses how partial reference alignments between ontologies may be leveraged for debugging taxonomies based on the "is-a" relation. The authors give algorithms for detecting and repairing missing "is-a" relations in an ontology, present a system implementing these algorithms, and report on experiments using the proposed debugging approach.

# Motivation 

Ontologies generally include some hierarchical structured knowledge of concepts. This hierarchical structure may be based on relations such as "is-a" or "is-part-of" and may be interpreted as a taxonomy. Such taxonomies often constitute an integral part of an ontology and plays a crucial role for its application case. Missing relations within a taxonomy can substantially affect the quality of an ontology both in terms of reasoning time and query results. Therefore, it is important to test and debug the structural information represented in ontologies.

# Detection Mechanism

In order to detect missing "is-a" relationships in an ontology the authors propose to leverage mappings between two ontologies, called _partial reference alignments_ (PRA), that associate concepts from one ontology with the other. If one ontology contains an "is-a" relationship between two concepts while the other ontology does not, then the latter is assumed to miss this "is-a" relationship. It is important to note that this approach makes two rather strong assumptions:

1. PRA, i.e. mappings between concepts of two ontologies, to are correct
2. Knowledge represented in ontologies is correct

This approach of detecting missing "is-a" relationship is generalised to work on a _network of ontologies_ in which all ontologies are pairwise interlinked by respective PRAs. The possibility of transitive detection mechanisms is not addressed. For example, consider three ontologies

\\[
\begin{align*}
O = \{A, B\}\\
O' = \{A', B'\}\\
O'' \{A'', B'', A'' \sqsubseteq B''
\end{align*}
\\]

and the following mappings

\\[
\begin{align*}
m: O \rightarrow O', A \mapsto A', B \mapsto B'\\
m': O \rightarrow O'', \emptyset\\
m'': O' \mapsto O'', A' \mapsto A'', B' \mapsto B''.
\end{align*}
\\]

Then, the proposed approach will detect a missing "is-a" relation for ontology \\( O'\\), but no missing "is-a" relations for ontology \\( O \\). However, the detection mechanism could be called again after the missing "is-a" relation in ontology \\(O'\\) is repaired, in which case it will detect now a missing relationship for ontology \\(O\\) as well.

# Repairing Mechanism

A _structural repair_ for an ontology with missing "is-a" relationships is defined to be a set of "is-a" relationships which, when added to the ontology, entail the originally missing relationships. Since this definition is rather general and allows for a multitude of potential repairing actions for an ontology, the authors also define a number of preference relations and heuristics that can guide the selection of structural repairs:

1. Subsets are preferred: Given two structural repairs. If one is a subset of the other, the former is preferred.
2. More information is preferred: Given two potential repair actions \\( x \text{ is-a } y \\) and \\(x' \text{ is-a } y'\\) for an ontology \\( O\\), then \\(x \text{ is-a } y \\) is preferred if \\(O \models x' \text{ \text{ is-a } } x \land y \text{ \text{ is-a } } y'\\)
3. Equivalences are to be avoided: Given two potential repair actions, such that one introduces an equivalence relationship whereas the other does not, then the later is preferred.

The first preference relation is intuitively comprehensible. The third preference relation is justified by the argument that equivalence relationships represent a strong assumption about the domain from a modelling perspective and should be treated with caution. The second preference relation is easily understandable by a mathematical reasoning: if \\(O \models x' \text{ is-a } x \land y \text{ is-a } y'\\) holds, then \\(x \text{ is-a } y \\) is _more informative_ than \\(x' \text{ is-a } y'\\) because we can derive \\(x' \text{ is-a } y' \\) once we have used \\(x \text{ is-a } y\\) to repair the missing relationship. Intuitively, If we need to repair a missing relationship \(( a \text{ is-a } b\\), then relating a superclass of \\(a\)) with subclass of \\(b\\) will fix the missing relationship indirectly by providing more specific information.


# Experimental results

I am unsure what the authors tried to show with their experiments. To be more precise, no research question has been formulated and I can only interpret the presented results as anecdotal evidence for the usefulness of the proposed debugging approach. The studies could have been designed to address issues mentioned in Section 5 concerning the selection of repairing actions based on the preference relations detailed above. Other important questions concern the practical impact of the proposed ranking on repairing actions (see Section 5.2) and the corresponding recommendations (see Section 5.3). Another interesting investigation would have been a detailed comparison of the "basic algorithm" (see Section 5.1.1) and the "extended algorithm" (see Section 5.1.2). Section 7.1.2 touches on the extended algorithm, but the reported numbers do not convey a thorough understanding of when or why to use or not to use the extended algorithm.

# Concluding remarks

The debugging approach is intuitively motivated and the underlying theory is presented in a clear but somewhat verbose manner. The debugging approach seems promising and sound from a theoretical point of view but a thorough experimental investigation for its practical usefulness is needed. After all, the approach is based on some very strong assumptions (PRA have to be correct, ontologies are assumed to truthfully represent their domain and are assumed to be always compatible via PRAs, theoretical expensive computational steps are claimed to be negligible in practice). 

# References

[^fn1]: Lambrix, Patrick & Liu, Qiang. (2013). Debugging the missing is-a structure within taxonomies networked by partial reference alignments. Data & Knowledge Engineering. 86. 179–205. 10.1016/j.datak.2013.    03.003.
