---
title: Causal knowledge extraction and Assembly Toolkit
has_children: true
nav_order: 2
---

# Overview
## World Modelers document management / reading / assembly / HMI workflows

Here we describe how to set up and run the systems responsible for
document corpus ingestion, machine reading, knowledge assembly, and human-machine
interface (HMI)-based exploration.

First, we describe running the full integrated system as a set of
interconnected Docker containers. Once running, this integrated system
allows for uploading documents through a web-based UI, having machine-reading
systems process these documents, and then creating an assembled knowledge
base that can be loaded into the CauseMos HMI. From the assembled knowledge
base, individual projects can be initiated and maintained. Uploading new
documents for a given project is also supported, with new causal knowledge
extracted from the documents incrementally added to the project.

In addition to the integrated system, we also document and provide
tutorials for running component technologies in simpler, more limited
workflows (W1-3). These workflows can be useful for prototyping changes
to component technologies before moving onto full integration, or for
situations where only a subset of component systems are needed.

<p align="center">
  <img src="images/workflows.png" width="500">
</p>

## Step-by-step tutorials

This section contains tutorials that each describe one specific
workflow on a set of publicly available sample documents. Users can follow
these tutorials step by step as a starting point and adapt them to
their own use cases.

- [Integrated workflow](reading-assembly/integrated_tutorial.md)

  In this tutorial, we provide a step-by-step example of running the integrated
  system as a set of Docker containers, uploading a handful of documents
  for processing, and then examining the resulting causal knowledge
  base extracted and assembled from these documents.

- [Reading and knowledge assembly tutorial](reading-assembly/w2_tutorial.html#w2)

  In this tutorial, we provide a step-by-step example of running
  a machine reading system on a set of sample documents and then running
  INDRA assembly on the outputs of the system.

## Running the integrated system


## Sub-system workflows
<a id="w1"></a>
### W1. Reading only

Machine-reading systems can be run independent of the integrated 
World Modelers system. In this case, users are responsible for preparing
input documents in an appropriate form and processing reading system
outputs for downstream usage.

The following pages provide detailed instructions for running each reading
system in a reading-only workflow:

  * [Eidos](reading-assembly/eidos.html#w1)
  * [HUME](reading-assembly/hume.html#w1)
  * [Sofia](reading-assembly/sofia.html#w1)

<a id="w2"></a>
### W2. Reading + integration/assembly

Running multiple reading systems on the same set of documents can provide
increased coverage and - through exploiting redundancy - a more reliable
knowledge base. INDRA World provides a programmatic interface for
working with reader outputs, combining extractions in a standardized
form, and running a variety of configurable processing and filtering
components to create a coherent knowledge base. This section describes
the usage of these components independent of the integrated system.

Systems used:
  * Readers: one or more of [Eidos](reading-assembly/eidos.html#w2), [HUME](reading-assembly/hume.html#w2), or [Sofia](reading-assembly/sofia.html#w2)
  * Integration/assembly: [INDRA](reading-assembly/indra.html#w2)

A step-by-step tutorial

<a id="w3"></a>
### W3. Document management + reading + integration/assembly
In this usage mode, the DART system is used for managing documents and using a standardized interface between DART and the reading systems. This avoids having to manually prepare input files for reading. The rest of the workflow follows W2 in that INDRA is used for integration. The user then takes INDRA Statements for further downstream analysis.

Systems used:
  * Document management: [DART](reading-assembly/dart.html#w3)
  * Readers: [Eidos](reading-assembly/eidos.html#w3), [HUME](reading-assembly/hume.html#w3), [Sofia](reading-assembly/sofia.html#w3)
  * Integration/assembly: [INDRA](reading-assembly/indra.html#w3)

<a id="w4"></a>
### W4. Document management + reading + integration/assembly + HMI
This usage mode goes beyond W2 or W3 by loading INDRA outputs into Causemos to explore, curate, and derive models from the assembled causal information. However, in this setting, the user is not expecting a service architecture to support incremental reading/assembly during runtime. The usage of DART is technically not required for W4 but it allows linking back to documents and examining their metadata which is advantageous. This workflow can be understood as a one-time run of W2/W3 and then loading results into the HMI as a “static” corpus.

Systems used:
  * Document management: [DART](reading-assembly/dart.html#w4)
  * Readers: [Eidos](reading-assembly/eidos.html#w4), [HUME](reading-assembly/hume.html#w4), [Sofia](reading-assembly/sofia.html#w4)
  * Integration/assembly: [INDRA](reading-assembly/indra.html#w4)
  * HMI: [Causemos](reading-assembly/causemos.html#w4)

<a id="w5"></a>
### W5. Document management + reading + integration/assembly + HMI + BYOD
This workflow builds on W4 and also enables users to add their own documents during runtime through Causemos. This requires DART, one or more readers, and INDRA World to be running as services.

Systems used:
  * Document management: [DART](reading-assembly/dart.html#w5)
  * Readers: [Eidos](reading-assembly/eidos.html#w5), [HUME](reading-assembly/hume.html#w5), [Sofia](reading-assembly/sofia.html#w5)
  * Integration/assembly: [INDRA](reading-assembly/indra.html#w5)
  * HMI: [Causemos](reading-assembly/causemos.html#w5)

## Component-specific documentation

* Readers
  * [Eidos](reading-assembly/eidos.html)

    Eidos is the machine reading system developed by the CLU lab at University of Arizona.
  
    Workflows: ([W1](reading-assembly/eidos.html#w1), [W2](reading-assembly/eidos.html#w2), [W3](reading-assembly/eidos.html#w3), [W4](reading-assembly/eidos.html#w4), [W5](reading-assembly/eidos.html#w5))

  * [HUME](reading-assembly/hume.html)
  
    Hume is BBN's machine reading system that extracts causal relations from text and supports clustering for ontology construction.
    
    Workflows: ([W1](reading-assembly/hume.html#w1), [W2](reading-assembly/hume.html#w2), [W3](reading-assembly/hume.html#w3), [W4](reading-assembly/hume.html#w4), [W5](reading-assembly/hume.html#w5))

  * [Sofia](reading-assembly/sofia.html)

    Sofia is a machine reading system developed at CMU that extracts causal relations from text.
  
    Workflows: ([W1](reading-assembly/sofia.html#w1), [W2](reading-assembly/sofia.html#w2), [W3](reading-assembly/sofia.html#w3), [W4](reading-assembly/sofia.html#w4), [W5](reading-assembly/sofia.html#w5))

* Integration/assembly
  * [Indra World](reading-assembly/indra.html)
  
    INDRA World is a knowledge assembly system that integrates causal relations extracted by multiple reading systems,
    standardizes their representation, finds ontological relationships between relations, calculates overall confidence,
    and has a configurable pipeline to process and filter causal knowledge.
  
    Workflows: ([W2](reading-assembly/indra.html#w2), [W3](reading-assembly/indra.html#w3), [W4](reading-assembly/indra.html#w4), [W5](reading-assembly/indra.html#w5))

* Document management
  * [DART](reading-assembly/dart.html)
  
    The Data Analytics and Reasoning Toolkit (DART) is the data ingestion pipeline for the World Modelers platform.
    
    Workflows: ([W3](reading-assembly/dart.html#w3), [W4](reading-assembly/dart.html#w4), [W5](reading-assembly/dart.html#w5))

* HMI (Human-Machine Interface)
  * [Causemos](reading-assembly/causemos.html)
  
    Causemos is the main HMI for the World Modelers program, built and maintained by Uncharted Software.
  
    Workflows: ([W4](reading-assembly/causemos.html#w4), [W5](reading-assembly/causemos.html#w5))
