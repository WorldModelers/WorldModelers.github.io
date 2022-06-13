---
title: Sofia Workflows
has_children: false
parent: Sofia
grand_parent: Causal Knowledge Extraction and Assembly Toolkit
nav_order: 1
---

# Sofia Workflows

## Contents
* [Integrated system](#integrated-system)
* [Reading and assembly](#reading-and-assembly)
* [Reading only](#reading-only)


<a id="integrated-system"></a>
### [Integrated system](index.html#integrated-system)
 
There are several caveats related to running Sofia as part of the integrated
system including the following.

1. **Ontology structure**

   `SOFIA` works with an older version of the World Modelers Ontology structure.
   The latest version of the ontologies used by the other Readers uses an
   updated format that is not natively recognized `SOFIA`. There is a CLI tool
   for translating the ontology into something `SOFIA` can use that is provided
   with the [DART Concepts Explorer](https://github.com/twosixlabs-dart/dart-ui)
   project. Any ontologies developed with the *Ontology in a Day (OIAD)*
   workflow must be run through this utility first before `SOFIA` can use it.
   Instructions for running this utility can be
   found [here](https://github.com/twosixlabs-dart/dart-ui#translate-backwards).

2. **No support for dynamic ontology loading**

   `SOFIA` can only support a single ontology per instance of the application.
   It loads a static resource from the filesystem on startup and has not been
   integrated with
   the [Ontology Registry](https://github.com/twosixlabs-dart/ontology-registry)
   . Furthermore, due to the necessity to adapt the ontology structure
   out-of-band, it is not currently possible to support the dynamic "hot
   swapping" of ontologies at runtime. Therefore, to utilize `SOFIA` to obtain
   Reader Outputs for the latest version of the *World Modelers Machine Reading
   Pipeline*, one of the following deployment scenarios must be chosen.

   a. Run multiple instances of the `SOFIA` application with different ontologies

   `SOFIA` can be run as a realtime stream processor if the ontologies are
   stable and provided ahead of time. Provided that the ontology has been
   properly translated, you can run a single instance of the `SOFIA` application
   for each ontology. The file is specified with the `ONTOLOGY` environment
   variable when starting the Docker container.

    b. Process the data "offline" in batches

    The `SOFIA` Reader can also be run
    as an offline batch process. This scenario is also contingent on a set of
    stable ontologies being available ahead of time. To support this scenario,
    one can run `SOFIA` with the `KAFKA_AUTO_OFFSERT_RESET` parameter set
    to `earliest` to force it to process the entire CDR update stream each
    time. `SOFIA` can be run once per ontology to produce the desired Reader
    Outputs.


At the time of writing, the changes necessary to run `SOFIA` with the latest World Modelers configuration has not been merged into the `master` branch. One must use a Docker image that is based off of [this fork](https://github.com/twosixlabs-dart/WM-src) or [this branch](TODO) of the main repository. The following Docker compose configuration can be used to run `SOFIA` in order to support both of the scenarios outlined above:

| Name                       | Description                                                          | Examples                                               |
| -------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------ |
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


<a id="reading-and-assembly"></a>
### [Reading and assembly](index.html#reading-and-assembly) Reading + integration/assembly

In this workflow, INDRA World is used to process the output files generated by Sofia.
You can follow the instructions [below](#reading-only) to produce the output
files first and then follow the INDRA World instructions to run assembly.
<a id="w1"></a>

<a id="reading-only"></a>
### [Reading only](index.html#reading-only)

In this workflow Sofia runs as a standalone reading system. Usage instructions
for running Sofia on input documents is provided [here](https://github.com/spilioeve/WM-src#usage).