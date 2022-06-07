---
title: Sofia
has_children: true
parent: Causal Knowledge Extraction and Assembly Toolkit
nav_order: 4
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
At the time of writing, the changes necessary to run `SOFIA` with the latest World Modelers configuration has not been merged into the `master` branch. One must use a Docker image that is based off of [this fork](https://github.com/twosixlabs-dart/WM-src) or [this branch](TODO) of the main repository. The following Docker compose configuration can be used to run `SOFIA` in order to support both of the scenarios outlined above:
| Name                       | Description                                                          | Examples                                               |
|----------------------------|----------------------------------------------------------------------|--------------------------------------------------------|
| DART_KAFKA_BROKER_URL      | hostname of the Kafka broker that hosts the DART CDR stream          | kafka.dart.worldmodelers.com                           |
| DART_READER_UPLOAD_API_URL | hostname of the DART Reader Output REST API                          | rest.dart.worldmodelers.com                            |
| DART_CDR_API_URL           | hostname of the DART CDR Retrieval REST API                          | rest.dart.worldmodelers.com                            |
| ONTOLOGY                   | fully qualified path to the ontology file (must be translated first) | /opt/app/conf/49277ea4-7182-46d2-ba4e-87800ee5a315.yml |
| SOFIA_USER                 | DART username for the SOFIA Reader                                   | sofia                                                  |
| SOFIA_PASS                 | DART password of the SOFIA Reader                                    | dart-password                                          |


```yaml
  sofia:
    container_name: sofia
    image: sofia:latest
    environment:
      KAFKA_BROKER: ${DART_KAFKA_BROKER_URL}:19092
      UPLOAD_API_URL: http://${DART_READER_UPLOAD_API_URL}:13337/dart/api/v1/readers/upload
      CDR_API_URL: http://${DART_CDR_API_URL}:8090/dart/api/v1/cdrs
      KAFKA_AUTO_OFFSET_RESET: earliest
      ONTOLOGY: /opt/app/conf/49277ea4-7182-46d2-ba4e-87800ee5a315.yml
      SOFIA_USER: sofia
      SOFIA_PASS: <SOFIA_DART_PASSWORD>
    restart: unless-stopped
    volumes:
     - ./data/sofia:/sofia
     - ./data/appdata:/opt/app/data
    network_mode: host
```

## Workflows

<a id="w1"></a>
### [W1](index.html#w1) Reading only

Documentation...

<a id="w2"></a>
### [W2](index.html#w2) Reading + integration/assembly

Documentation...

<a id="w3"></a>
### [W3](index.html#w3) Document management + reading + integration/assembly

Documentation...

<a id="w4"></a>
### [W4](index.html#w4) Document management + reading + integration/assembly + HMI

Documentation...

<a id="w5"></a>
### [W5](index.html#w5) Document management + reading + integration/assembly + HMI + BYOD

Documentation...
