---
layout: default
title: INDRA
parent: Modeling Systems
nav_order: 4
---

# Project Overview

<img src="http://www.indra.bio/doc/indra_logo.png?raw=True" width="300" height="224" align="left" style="margin-right: 10px; margin-bottom: 5px;">
INDRA (Integrated Network and Dynamical Reasoning Assembler) is an automated model assembly system, originally developed for molecular systems biology and currently being generalized to other domains. INDRA draws on natural language processing systems and structured databases to collect mechanistic and causal assertions, represents them in a standardized form (INDRA Statements), and assembles them into various modeling formalisms including causal graphs and dynamical models. INDRA also provides knowledge assembly procedures that operate on INDRA Statements and correct certain errors, find and resolve redundancies, infer missing information, filter to a scope of interest and assess belief.

* Project website: [http://www.indra.bio/](http://www.indra.bio/)
* Project maintainer: [Harvard Medical School's Sorger Lab](https://sorger.med.harvard.edu/)
* Points of contact: [Ben Gyori (@bgyori)](https://github.com/bgyori)

## World Modelers Integration

INDRA functions as a hub between World Modelers machine reading systems and the other modeling systems. It provides a convenient API to submit text for machine reading to the primary World Modelers readers: [Eidos](../readers/eidos.md), [Sofia](../readers/sofia.md), and [Hume](../readers/hume.md).

INDRA uses extractions from machine reading to generate causal statements in its standardized form, the INDRA statement. INDRA statements are then used by other modeling systems, such as [Delphi](delphi.md) and [DySE](dyse.md) to generate predictive analyses.

Currently, INDRA is deployed as a REST API which is available at [http://api.indra.bio:8000](http://api.indra.bio:8000) with documentation at [http://www.indra.bio/rest_api/docs](http://www.indra.bio/rest_api/docs). Note that the REST API is ideal for prototyping and for building light-weight web apps, but should not be used for large reading and assembly workflows.

## Getting Started

Installation instructions for INDRA are available in [its Github repository](https://github.com/sorgerlab/indra#installation) and detailed usage [documentation is available here](https://indra.readthedocs.io/en/latest/installation.html).