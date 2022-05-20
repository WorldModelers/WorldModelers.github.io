---
title: Causemos
has_children: false
parent: Causal Knowledge Extraction and Assembly Toolkit
nav_order: 6
---

# Causemos HMI

In Causemos, individual analysts or analytical teams work in an
**Analysis Project**. When creating a new Analysis Project, you select
the **Knowledge Base** containing the literature relevant to the
analysis domain(s).

Some metadata about the Knowledge Base is visible on the Project page:
name, number of documents, and number of causal relationships extracted
from these documents.

![Knowledge Base metadata on the Project page](../images/causemos/image23.jpg)

Analysts can upload additional documents to the project knowledge base
and use the extracted relations.

![Analysts can upload documents such as PDFs to the Knowledge Base and then filter the Knowledge Base Explorer to see causal statements extracted from them.](../images/causemos/image19.jpg)


# Workflows

<a id="w4"></a>
## [W4](index.html#w4) Document management + reading + integration/assembly + HMI
In this workflow, Causemos ingests, combines and enriches an INDRA statements dataset and a DART CDR dataset to create a new Knowledge Base dataset.

Here is an abridged and lightweight version of using Causemos as a knowledge explorer, for more detail on a complete Causemos install please consult the [full documentation](https://github.com/uncharted-causemos/quickstart#loading-knowledge-data).


Start an ElasticSearch instance

```
docker run --name es01 --net elastic -p 9200:9200 -p 9300:9300 -it docker.elastic.co/elasticsearch/elasticsearch:7.17.3
```

Load index mappings

```
git clone git@github.com:uncharted-causemos/atlas.git

cd atlas

ES=<elastic_url> python ./es_mapper.py
```


To start Causemos with knowledge explorer 

```
# 1. Clone quick start
git clone git@github.com:uncharted-causemos/quickstart.git

cd app-kb

# 2. Update configuration files under env

# 3. Start docker
docker-compose up
```
Causemos should be available on http://localhost:3003


Then to load data into Causemos

```
# Clone knowledge pipeline
git clone git@github.com:uncharted-causemos/anansi.git

pip install -r requirements.txt
```

Then run the provided script to load IDNRA and DART datasets as a knowledge base in Causemos, for our purpose here SOURCE and TARGET are the same.

```
#!/usr/bin/env bash

SOURCE_ES=xyz \
SOURCE_USERNAME=xyz \
SOURCE_PASSWORD=xyz \
TARGET_ES=xyz \
TARGET_USERNAME=xyz \
TARGET_PASSWORD=xyz \
DART_DATA=<path_to_dart_cdr.json> \
INDRA_DATASET=<path_to_indra_directory> \
python src/knowledge_pipeline.py
```



<a id="w5"></a>
### [W5](index.html#w5) Document management + reading + integration/assembly + HMI + BYOD
In this workflow, it is assumed that both INDRA and DART are running as web services.
TODO
