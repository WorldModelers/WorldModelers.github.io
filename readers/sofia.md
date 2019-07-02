---
layout: default
title: SOFIA
parent: Reading Systems
nav_order: 3
---

This is a placeholder for SOFIA.

## Project Overview

SOFIA is a machine reading and annotation tool developed by [Carnegie Mellon University](https://www.cmu.edu/). It extracts causal relations from text and also enables a query based approach to causal extraction. 

* Project website: Coming soon
* Project maintainer: [Carnegie Mellon University](https://www.cmu.edu/)
* Points of contact: [Evangelia Spiliopoulou
    ](mailto:espiliop@andrew.cmu.edu)

## World Modelers Integration

Currently, SOFIA is run as standalone software. Output from SOFIA reading is stored in JSON-LD format and can be used by Hume for model assembly. SOFIA is service enabled and text can be submitted to it through a [REST API available here](https://sofia.worldmodelers.com/ui/) (credentials available upon request).


## Getting Started

Currently, SOFIA is not open source. It can be run via Docker and appropriate quick start information will be posted here once it is available. You may choose to interact with SOFIA via its [REST API](https://sofia.worldmodelers.com/ui/) but will first need to request credentials for authorization. 

If you have credentials, you can interact with SOFIA (`Python`) with:

```
import requests
url = 'https://sofia.worldmodelers.com'

# process_text 
obj = {'text': 'The intense rain caused flooding in the area and in the capital'}
response = requests.post(url + '/process_text', json=obj, auth=('USER','PASSWORD'))

# process_query
obj = {'text': 'The intense rain caused flooding in the area and in the capital',
       'query': ['food security', 'malnutrition', 'starvation', 'famine', 'flood']}
response = requests.post(url + '/process_query', json=obj, auth=('USER','PASSWORD'))

response = response.json()
```