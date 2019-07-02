---
layout: default
title: CWMS
parent: Reading Systems
nav_order: 4
---

## Project Overview

CWMS is an extension of TRIPS and is developed by the Florida Institue for Human & Machine Cognition (IHMC). CWMS offers deep natural language understanding and extraction of causal relations from text. It also provides the capability to extract structured data from tables embedded within PDFs and other documents.

* Project website: [http://trips.ihmc.us/parser/cgi/cwmsreader](http://trips.ihmc.us/parser/cgi/cwmsreader)
* Project maintainer: [IHMC](ihmc.us)
* Points of contact: [Lucian Galescu](mailto:lgalescu@ihmc.us)

## World Modelers Integration

CWMS is invoked using IHMC's [TRIPS Web API](http://trips.ihmc.us/parser/api.html). It can be invoked through [INDRA](http://indra.readthedocs.io/) or as a standalone component.

## Getting Started

Text can easily be submitted to the live CWMS endpoint available through the INDRA API. To do this, you can try (using `Python`):

```
import requests

url = 'http://api.indra.bio:8000'
endpoint = '/cwms/process_text'

text = '''
          Flooding in the region caused significant instability. Furthermore, it reduced aid workers capacity to assist due to the damage caused to roadways.
       '''

response = requests.post(url+endpoint, json={'text': text})
cwms_statements = response.json()
print(cwms_statements['statements'][0])

Out:

{'belief': 1,
 'evidence': [{'epistemics': {'direct': False},
   'pmid': 'TEXT00017_IO-54919',
   'source_api': 'cwms',
   'source_hash': -792766597917711571,
   'text': 'Flooding in the region caused significant instability.',
   'text_refs': {'PMID': 'TEXT00017_IO-54919'}}],
 'id': '0207dd21-e61b-486c-b8aa-c09519c0d7a8',
 'obj': {'db_refs': {'CWMS': 'ONT::NOT-STEADY-SCALE',
   'TEXT': 'significant instability'},
  'name': 'significant instability'},
 'obj_delta': {'adjectives': [], 'polarity': 1},
 'subj': {'db_refs': {'CWMS': 'ONT::ARRIVE', 'TEXT': 'Flooding in the region'},
  'name': 'Flooding in the region'},
 'subj_delta': {'adjectives': [], 'polarity': None},
 'type': 'Influence'}
```