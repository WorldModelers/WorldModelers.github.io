---
layout: default
title: Eidos
parent: Reading Systems
nav_order: 1
---

## Project Overview

Eidos is an open-domain machine reading system designed by the [Computational Language Understanding (CLU) Lab](http://clulab.cs.arizona.edu/) at University of Arizona for the World Modelers DARPA program. It uses a cascade of [Odin](https://github.com/clulab/processors) grammars to extract events from free text.

Eidos identifies entities like "food insecurity" along with a growing list of arguments on those entities, such as increases / decreases / quantifications. It subsequently detects events that occur between entities (directed causal events, for example) as in "food insecurity causes increased migration". The list of arguments and events is updated frequently and is documented on the [JSON-LD](https://github.com/clulab/eidos/wiki/JSON-LD) page.

* Project website: [https://github.com/clulab/eidos](https://github.com/clulab/eidos)
* Project maintainer: [Computational Language Understanding (CLU) Lab](http://clulab.cs.arizona.edu/) at University of Arizona
* Points of contact: [Mihai Surdeanu](mailto:msurdeanu@email.arizona.edu)

## World Modelers Integration

Eidos provides a fast API for extracting causal relations from text. It is integrated directly with [INDRA](http://indra.readthedocs.io/) or can be run as a standalone system or as a [web service](https://github.com/clulab/eidos#web-service).


## Getting Started

The quickest way to interact with Eidos is to build its Docker container and run it, using the [instructions provided here](https://github.com/clulab/eidos/tree/master/Docker). Once you have the Docker container running, you may send text to it using the following (`Python`) example:

```
import requests

text = '''
          Flooding in the region caused significant instability. Furthermore, it reduced aid workers capacity to assist due to the damage caused to roadways.
       '''

webservice = 'http://localhost:9000'
res = requests.post('%s/process_text' %webservice, headers={'Content-type': 'application/json'}, json={'text': text})

json_dict = res.json()
```