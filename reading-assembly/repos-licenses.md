---
layout: default
title: Repository Overview and Licenses
parent: Causal Knowledge Extraction and Assembly Toolkit
nav_order: 10
has_toc: true
---

## Reading and knowledge assembly software

### Eidos

Eidos is the machine reading system developed by the CLU lab at University of Arizona. This repository includes the reading software as well as code for integrating with DART.

- Repository: [https://github.com/clulab/eidos](https://github.com/clulab/eidos)
- License:
  - While we will soon be licensed as Apache, currently one dependency has a GPL license. This will be removed very soon and the license will be updated.
  - Otherwise, [https://github.com/clulab/eidos/blob/master/LICENSE](https://github.com/clulab/eidos/blob/master/LICENSE)
- Documentation: [https://github.com/clulab/eidos/wiki](https://github.com/clulab/eidos/wiki), [https://github.com/clulab/eidos#readme](https://github.com/clulab/eidos#readme)
- Stable version: [https://github.com/clulab/eidos/releases/tag/latest](https://github.com/clulab/eidos/releases/tag/latest)
- Versions available on Maven Central: [https://mvnrepository.com/artifact/org.clulab/eidos](https://mvnrepository.com/artifact/org.clulab/eidos)

### Concept Discovery

This is the concept identification component, which is used by the ontology-in-a-day (OIAD) system.

- Repository: [https://github.com/clulab/conceptdiscovery/](https://github.com/clulab/conceptdiscovery/)
- License
  - While we will soon be licensed as Apache, currently one dependency has a GPL license. This will be removed very soon and the license will be updated.
  - Otherwise, [https://github.com/clulab/conceptdiscovery/blob/master/LICENSE](https://github.com/clulab/conceptdiscovery/blob/master/LICENSE)
- Documentation: [https://github.com/clulab/conceptdiscovery/#readme](https://github.com/clulab/conceptdiscovery/#readme)
- Stable version: [https://github.com/clulab/conceptdiscovery/releases/tag/latest](https://github.com/clulab/conceptdiscovery/releases/tag/latest)
- Versions available on Maven Central: [https://mvnrepository.com/artifact/org.clulab/conceptdiscovery](https://mvnrepository.com/artifact/org.clulab/conceptdiscovery)

### HUME

Hume is BBN's machine reading system that extracts CAGs and supports the OIAD clustering. It leverages the following software
- Repository: [https://github.com/BBN-E/Hume](https://github.com/BBN-E/Hume)
- License: Apache [https://github.com/BBN-E/Hume/blob/master/LICENSE](https://github.com/BBN-E/Hume/blob/master/LICENSE)
- Documentation: [https://github.com/BBN-E/Hume/blob/master/README.md](https://github.com/BBN-E/Hume/blob/master/README.md)
- Stable version: TODO

Text-Open contains Java and Python APIs for reading and writing BBN's SerifXML format, which is BBN's internal representation of documents and information.
- Repository: [https://github.com/BBN-E/text-open](https://github.com/BBN-E/text-open)
- License: Apache [https://github.com/BBN-E/text-open/blob/main/LICENSE](https://github.com/BBN-E/text-open/blob/main/LICENSE)
- Documentation: [https://github.com/BBN-E/text-open/blob/main/README.md](https://github.com/BBN-E/text-open/blob/main/README.md)
- Stable version: TODO

LearnIt is a tool for customizing Machine Readers (a.k.a., Information Extraction algorithms) with human in the loop. Within WM, we also use it as a pattern-based extractor for event extraction.
- Repository: [https://github.com/BBN-E/LearnIt](https://github.com/BBN-E/LearnIt)
- License: Apache [https://github.com/BBN-E/LearnIt/blob/master/LICENSE](https://github.com/BBN-E/LearnIt/blob/master/LICENSE)
- Documentation: [https://github.com/BBN-E/LearnIt/blob/master/README.md](https://github.com/BBN-E/LearnIt/blob/master/README.md)
- Stable version:  [https://github.com/BBN-E/LearnIt](https://github.com/BBN-E/LearnIt)

NLPLingo is BBN's Deep Learning toolkit for event extraction and causal relation extraction.
- Repository: [https://github.com/BBN-E/nlplingo](https://github.com/BBN-E/nlplingo)
- License: Apache [https://github.com/BBN-E/nlplingo/blob/main/LICENSE](https://github.com/BBN-E/nlplingo/blob/main/LICENSE)
- Documentation: [https://github.com/BBN-E/nlplingo/blob/main/README.md](https://github.com/BBN-E/nlplingo/blob/main/README.md)
- Stable version: [https://github.com/BBN-E/nlplingo](https://github.com/BBN-E/nlplingo)

CSerif contains C/C++ code for pre-reading of texts into BBN's SerifXML format. We are working on open sourcing this.
- Repository: [https://github.com/BBN-E/serif](https://github.com/BBN-E/serif)
- License: Apache [https://github.com/BBN-E/serif/blob/master/LICENSE](https://github.com/BBN-E/serif/blob/master/LICENSE)
- Documentation: [https://github.com/BBN-E/serif/blob/master/README.md](https://github.com/BBN-E/serif/blob/master/README.md)
- Stable version: [https://github.com/BBN-E/serif](https://github.com/BBN-E/serif)

### Sofia

- Repository: [https://github.com/spilioeve/WM-src](https://github.com/spilioeve/WM-src)
- License: MIT License
- Documentation: [https://github.com/spilioeve/WM-src/blob/master/README.md](https://github.com/spilioeve/WM-src/blob/master/README.md)
- Stable version: [https://github.com/spilioeve/WM-src](https://github.com/spilioeve/WM-src)

### INDRA World

- Repository: [https://github.com/indralab/indra_world](https://github.com/indralab/indra_world)
- License: BSD 2-Clause License
- Documentation: [https://indra-world.readthedocs.io/en/latest/](https://indra-world.readthedocs.io/en/latest/)
- Stable version: [https://github.com/indralab/indra_world/releases/tag/march_2022_embed](https://github.com/indralab/indra_world/releases/tag/march_2022_embed)

## Ontology

The reading and assembly software developed under World Modelers program share the same underlying ontology.

- Repository: [https://github.com/WorldModelers/Ontologies](https://github.com/WorldModelers/Ontologies)
- License:
  - Ontologies: [https://github.com/WorldModelers/Ontologies/blob/master/LICENSE.txt](https://github.com/WorldModelers/Ontologies/blob/master/LICENSE.txt)
  - Code: [https://github.com/WorldModelers/Ontologies/blob/master/common/src/main/resources/LICENSE.txt](https://github.com/WorldModelers/Ontologies/blob/master/common/src/main/resources/LICENSE.txt)
- Documentation: [https://github.com/WorldModelers/Ontologies/blob/master/README.md](https://github.com/WorldModelers/Ontologies/blob/master/README.md)
- Stable version: [https://github.com/WorldModelers/Ontologies/tags/latest](https://github.com/WorldModelers/Ontologies/tags/latest)
