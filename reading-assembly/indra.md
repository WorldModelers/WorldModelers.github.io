---
title: INDRA World
has_children: true
parent: Causal Knowledge Extraction and Assembly Toolkit
nav_order: 5
has_toc: false
---
# INDRA World

<img align="left" style="padding-right: 10px;" src="https://raw.githubusercontent.com/indralab/indra_world/master/doc/indra_world_logo.png" width="300" height="160" />
INDRA World is a knowledge assembly system that takes as input causal relations
extracted by one or more reading systems from text. INDRA World first processes
the output of reading systems into a standardized object model called INDRA
Statements and then performs a number of assembly operations on Statements.
An INDRA assembly pipeline can be configured flexibly to apply various
filters (for quality, relevance, etc.), normalization, and processing steps.

INDRA World builds on and is a generalization of INDRA, a knowledge and model
assembly system originally developed for biology. INDRA World makes use of the
general INDRA assembly logic to find relationships between Statements,
including matching, contradiction, and refinement (i.e., one statement is a
more general or more specific version of the other). These inter-Statement
relations are reconstructed with respect to an ontology graph and INDRA World
uses a scalable algorithm that can handle finding relations between
tens of millions of Statements. Statements that match
exactly are merged and their supporting evidences are combined. Stateements
that are in a refinement relationship where one is a specification or
a generalization of the other are organized into a refinement graph.
Given the overall direct or indirect support for a Statement, INDRA World
uses a probabilistic "belief" model to determine how likely it is that
the Statement is correct (i.e., not a result of a reading error) and assigns
a score between 0 and 1.

After the assembly process, INDRA Statements can be used directly programmatically
or interactively through visual interfaces such as CauseMos. They are also
the basis of qualitative analysis and serve as input to the DySE and Delphi
systems which turn collections of assembled INDRA Statements into
Boolean models and Dynamic Bayesian Networks, respectively.

Importantly, INDRA World implements a service architecture which allows it
perform incremental assembly in a project-specific way.
For example, an initial assembly  produced by INDRA World might have
incorporated reader output for 10k documents (which comes at a large initial
reading and processing cost), and later 10 more documents need to be added
to the same project. The INDRA World REST API can incorporate reader
outputs for these new documents and produce an "assembly delta" which
describes how the structure of Statements, their relationships, their
supporting evidences, as well as Statement beliefx change as a result
of the new relations extracted from the documents.

The INDRA World documentation is available [here](https://indra-world.readthedocs.io/en/latest/).
