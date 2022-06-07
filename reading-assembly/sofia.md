---
title: Sofia
has_children: true
parent: Causal Knowledge Extraction and Assembly Toolkit
nav_order: 4
has_toc: false
---
# Sofia

SOFIA is an Information Extraction system whose main goal is to extract Causal
Relations that are explicitly mentioned in text, in order to facilitate
automatic causal analysis graph construction.

SOFIA extracts three major types of information: Entities, Events, and
Causal-type Relations. All semantic units are important in order to build a
coherent model useful for CAG construction. Entities include physical objects,
people, organizations, etc., while events denote some actions, processes or
changes of state. Entities are participants in events (e.g., the car moves),
while events are arguments to relations like Causality (e.g., Reading causes
Thinking).

The detected Events and Entities are currently grounded to SOFIA's internal
Ontology, We note that although the Ontology is subject to minor changes, we do
not plan to change the Upper Level structure. Additional information provided by
SOFIA includes Time, Location, Confidence Scores and Quantitative/Qualitative
metrics of Entities.


## Disclaimer

Development of the `SOFIA` Reader ended before a few key features were
introduced to the World Modelers Machine Reading Pipeline. As a result, there
are a number of caveats that must be taken into account in order to use `SOFIA`
to produce reader outputs. For more details, see the [Sofia Workflows](sofia_workflows.html)
page.
