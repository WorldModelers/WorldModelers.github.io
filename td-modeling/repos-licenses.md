---
layout: default
title: Repositories and Licenses
parent: Qualitative Analysis Toolkit
has_toc: true
nav_order: 5
---

# Top-Down Modeling Repositories
World Modelers repositories related to top-down modeling/analysis engines and the aspects of the human-machine interface supporting this functional area

## Engine Software Components

### Delphi

University of Arizona's top-down modeling engine. 
- Repository: See [https://ml4ai.github.io/delphi/index.html](https://ml4ai.github.io/delphi/index.html) for more information.
- License: Apache, see [https://ml4ai.github.io/delphi/index.html#license-and-funding](https://ml4ai.github.io/delphi/index.html#license-and-funding)
- To run Delphi independently as a standalone engine without the HMI, here are the installation/configuration instructions: [https://worldmodelers.com/td-modeling/delphi.html#running-locally-without-the-hmi](https://worldmodelers.com/td-modeling/delphi.html#running-locally-without-the-hmi)
- To run Delphi with the Causemos HMI, here are the installation/configuration instructions: [https://docs.google.com/presentation/d/19PeNAoCIxNCQxXAZNV4Gn4kMVPCAJKYlLXQCJ6V2SZM/edit#slide=id.g8c51928f8f_0_200](https://docs.google.com/presentation/d/19PeNAoCIxNCQxXAZNV4Gn4kMVPCAJKYlLXQCJ6V2SZM/edit#slide=id.g8c51928f8f_0_200)

### DySE

University of Pittsburgh's top-down modeling engine. 
- Repository: See [https://github.com/pitt-miskov-zivanov-lab/dyse_wm](https://github.com/pitt-miskov-zivanov-lab/dyse_wm) for more information.
- License: MIT, see [https://github.com/pitt-miskov-zivanov-lab/dyse_wm/blob/main/LICENSE.txt](https://github.com/pitt-miskov-zivanov-lab/dyse_wm/blob/main/LICENSE.txt)
- To run DySE independently as a standalone engine without the HMI, here are the installation/configuration instructions: [https://github.com/pitt-miskov-zivanov-lab/dyse_wm/blob/main/README.md](https://github.com/pitt-miskov-zivanov-lab/dyse_wm/blob/main/README.md)
- To run DySE with the Causemos HMI, here are the installation/configuration instructions: PLACEHOLDER, include all repositories needed

### Sensei

[Jataware](https://jataware.com/)'s top-down modeling engine. 
- Repository: See [https://github.com/dojo-modeling/sensei](https://github.com/dojo-modeling/sensei) for more information.
- License: MIT, see [https://github.com/dojo-modeling/sensei/blob/main/LICENSE](https://github.com/dojo-modeling/sensei/blob/main/LICENSE)
- Running Sensei independently as a standalone engine and with the Causemos HMI requires the same setup steps, which are available [here](https://github.com/dojo-modeling/sensei#installation-and-setup).


## HMI Software Components
Causemos is the main user-interface in the WorldModelers program, used to synthesize knowledge into runnable graphs, and dervie additional insights using these engines.


### API
The API and data-exchange format can be found in
- https://github.com/uncharted-causemos/docs/tree/master/td-models

### Causemos
Causemos is split into the following modules to support top-down modeling:
- HMI: [https://github.com/uncharted-causemos/causemos](https://github.com/uncharted-causemos/causemos)
- Causemos data service: [https://github.com/uncharted-causemos/wm-go](https://github.com/uncharted-causemos/wm-go)
- Causemos recommendation service: [https://github.com/uncharted-causemos/wm-curation-recommendation](https://github.com/uncharted-causemos/wm-curation-recommendation)
- Unstructured extraction pipeline: [https://github.com/uncharted-causemos/anansi](https://github.com/uncharted-causemos/anansi)
- Structured data pipeline: [https://github.com/uncharted-causemos/slow-tortoise](https://github.com/uncharted-causemos/slow-tortoise)
- License:

#### Installation

Causemos requires:

- Elasticsearch with compatible dataset ingested (See [Corpus Ingestion
  and Assembly](../reading-assembly.html))
- At least one working inference engine, either external or hosted
  locally
