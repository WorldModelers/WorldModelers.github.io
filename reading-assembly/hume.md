---
title: HUME
has_children: false
parent: Corpus Ingestion and Assembly Toolkit
nav_order: 3
---
# HUME

## Workflows

<a id="w1"></a>
### [W1](index.html#w1) Reading only

In this workflow Hume runs as a standalone reading system.

#### System Preparation

For this mode, you will need to prepare a folder of CDR files (a richer article representation from DART), a ontology metadata file, and a config file.

You will also need to create a new working folder, we'll use `runtime` as an example in this document.

##### CDR Files

Detailed information of the schema of CDR can be found from DART side. For Hume's purposes, the fields below are required:

```json
{
  "document_id": "required,str: unique identifier of article",
  "source_uri": "optional,str: how to fetch the document",
  "extracted_metadata": {
    "Author": "optional,str: author of article",
    "CreationDate": "optional,str: in '%Y-%m-%d' without quote format. Will help time resolution if provided",
    "Pages": "optional,int: Will help for genre determination"
  },
  "extracted_text": "required,str: original text of article",
  "content_type": "optional,str: mime_type string, will be used genre determination"
}
```

Files should be named `[document_id].json`, where `[document_id]` is replaced with the actual document_id.

Copy all json files into your `runtime/corpus` directory.

##### Ontology Metadata File

The ontology metadata file should be formatted according to the following schema: https://github.com/WorldModelers/Ontologies/blob/master/CompositionalOntology_metadata.yml

##### Docker Config File

The config file is a json file that must be visible at runtime from `/extra/config.json` inside the container. An example is provided as follows:

```json
{
  "hume.domain": "WM",
  "hume.num_of_vcpus": "int, required: Number of cpu cores available to you. It at least needs to be 2, and please only include number of physical cores instead of SMT cores.",
  "hume.tmp_dir": "required,str: a bind point for sharing data in between your local system and docker instance",
  "hume.manual.cdr_dir": "required,str: A path, from inside docker that contains dir of docs you want to process, if you're following above, it should be /extra/corpus",
  "hume.manual.keep_pipeline_data": "optional,bool default to false: when enabled, we'll keep intermediate process file in between runs so you don't start from beginning. But if your previous run is finished and you'll kick off the new run, please set it to false for removing intermediate process file and run everything from scratch.",
  "hume.external_ontology_path": "optional, str: When provided, hume will use the ontology metadata file you provided instead of pre-shipped one. This path needs to be accessible from inside docker",
  "hume.external_ontology_version": "optional, str, but mandatory when you specify hume.external_ontology_path: id of the external ontology",
  "hume.use_regrounding_cache": "bool, optional: When enabled, the system will save intermediate files of processing result into a directory that if we see the same document later, we can skip certain processing steps and only kick off regrounding pipeline.",
  "hume.regrounding_cache_path": "str, required when hume.use_regrounding_cache is true: a persist directory for hosting regrounding cache. Ideally to be a persist storage that can be shared in between docker instances. Also please don't reuse grounding cache from OIAD."
}
```

Please copy the config file to `runtime/config.json`

#### To Run the Hume System

Run Hume with the following command:

```bash
docker run -it -v runtime:/extra docker.io/wmbbn/hume:R2022_03_21 /usr/local/envs/py3-jni/bin/python3 /wm_rootfs/git/Hume/src/python/dart_integration/manual_processing.py
```

After the run finishes, the results will be accessible at `[hume.tmp_dir]/results/[TIMESTAMP]/results`. The resulting output will be in JSON-LD format, as described [here](https://github.com/BBN-E/Hume/wiki#output-format-json-ld).

#### Example Workflow

In this example, we provide step-by-step instructions for running the Hume machine reading system on a set of sample documents.

In the steps below, we assume that our working folder is `runtime`, that this folder already exists and all work is done under this path. This is arbitrary and can be replaced by another appropriate local path.

This example assumes that the image for the Hume container has already been downloaded from [Docker hub](https://hub.docker.com/r/wmbbn/hume).

##### 1. Download sample documents
As a first step, we need to identify a set of sample documents to use as input. The World Modelers demo set of documents are publicly available on [Github](https://github.com/twosixlabs-dart/world-modelers-demo-docs). The demo document set includes both the raw source documents and the CDR files which contain both the text of the raw documents and some metadata. In this example we'll use the CDRs as input to Hume.

```bash
cd runtime
git clone https://github.com/twosixlabs-dart/world-modelers-demo-docs.git
```

The input documents will now be in the `runtime/world-modelers-demo-docs/cdrs` folder.

##### 2. Configure the Ontology
For the purposes of this example, we assume the latest version of [the default World Modelers ontology](https://github.com/WorldModelers/Ontologies/blob/master/CompositionalOntology_metadata.yml) will be used. Normally, if using this ontology, no extra steps are needed, however, here we make its use explicit to better illustrate how a custom ontology could be used.

We will put the ontology in `runtime/ontology.yml`, the following command doing the download:

```
wget https://raw.githubusercontent.com/WorldModelers/Ontologies/master/CompositionalOntology_metadata.yml -O runtime/ontology.yml
```

##### 3. Create an output directory
Create an output directory inside the working folder so that it can be accessed by both the local system and the docker instance.

```bash
mkdir runtime/output
```
##### 4. Create a Docker config file
Next we use a text editor to create a configuration file in `runtime/config.json` that tells Hume where to look for the input documents and ontology. The contents of the file should be as follows:

```
{
  "hume.domain": "WM",
  "hume.num_of_vcpus": 4,
  "hume.tmp_dir": "/extra/output",
  "hume.manual.cdr_dir": "/extra/world-modelers-demo-docs/cdrs",
  "hume.external_ontology_path": "/extra/ontology.yml",
  "hume.use_regrounding_cache": false
}
```

In this example we assume a system with access to 4 physical CPU cores. The `hume.num_of_vcpus` setting may need to be adjusted to reflect your own hardware specs.

##### 5. Run Hume on the documents
Finally, we run Hume on the input documents. Hume will write its output to the `runtime/output/results/$TIMESTAMP/results` folder, where `$TIMESTAMP` refers to a string representing the date/time of the run.

Note: In the command below, replace the `$RUNTIME` variable with the absolute path of your `runtime` folder (for example `/home/wmuser/runtime`).

```bash
docker run -it -v $RUNTIME:/extra docker.io/wmbbn/hume:R2022_03_21 /usr/local/envs/py3-jni/bin/python3 /wm_rootfs/git/Hume/src/python/dart_integration/manual_processing.py
```

Reading can take a few hours. For faster results, start with an input folder that only contains a subset of CDRs.

<a id="w2"></a>
### [W2](index.html#w2) Reading + integration/assembly

The W2 workflow is achieved by following the instructions for [W1](hume.html#w1) above and then referring the INDRA instructions for [W2](indra.html#w2).

<a id="w3"></a>
### [W3](index.html#w3) Document management + reading + integration/assembly

In this workflow, Hume is integrated with DART and INDRA in a BYOD system.

#### System Preparation

For this mode, you will need to prepare a config file.

You will also need to create a new working folder, we'll use `runtime` as an example in this document.

##### Docker Config File

The config file is a json file that must be visible at runtime from `/extra/config.json` inside the container. It's modified from https://github.com/twosixlabs-dart/python-kafka-consumer/blob/master/pyconsumer/resources/env/test.json. An example is provided as follows:

Note: Do not change unannotated fields in the example unless you really know what you're doing.

```json
{
  "kafka.bootstrap.servers": "str,required: example is wm-ingest-pipeline-streaming-1.prod.dart.worldmodelers.com:9093",
  "auth": {
    "username": "str,required. If auth is not required, please delete auth dict directly",
    "password": "str,required"
  },
  "app": {
    "id": "hume",
    "auto_offset_reset": "earliest",
    "enable_auto_commit": false
  },
  "topic": {
    "from": "str,required: topic to listen to from kafka"
  },
  "CDR_retrieval": "str,required: example is https://wm-ingest-pipeline-rest-1.prod.dart.worldmodelers.com/dart/api/v1/cdrs",
  "DART_upload": "str,required: example is https://wm-ingest-pipeline-rest-1.prod.dart.worldmodelers.com/dart/api/v1/readers",
  "Ontology_retrieval": "str,required: example is https://wm-ingest-pipeline-rest-1.prod.dart.worldmodelers.com/dart/api/v1/ontologies",
  "DART_upload_labels": [
    "from_docker"
  ],
  "hume.domain": "WM",
  "hume.num_of_vcpus": "int, required: Number of cpu cores available to you. It at least needs to be 2, and please only include number of physical cores instead of SMT cores.",
  "hume.tmp_dir": "required,str: a bind point for sharing data in between your local system and docker instance",
  "hume.streaming.mini_batch_size": "int, required: For streaming mode, this deterimines the size of a mini batch (which is used for improved efficiency)",
  "hume.streaming.mini_batch_wait_time": "int, required: For streaming mode, even if we received fewer documents than mini_batch_size, the system will start processing after mini_batch_wait_time seconds.",
  "hume.streaming.keep_pipeline_data": "bool, optional: When enabled all intermediate files during processing will be preserved. This is mainly a debugging switch for developer.",
  "hume.streaming.skip_processed": "bool, optional: When enabled, we'll keep a record of processed (document_id, ontology_id) tuples in a file under hume.tmp_dir/processed.log and if we see the same kafka reading request, we'll ignore it. ",
  "hume.use_regrounding_cache": "bool, optional: When enabled, the system will save intermediate files of processing result into a directory that if we see the same document later, we can skip certain processing steps and only kick off regrounding pipeline.",
  "hume.regrounding_cache_path": "str, required when hume.use_regrounding_cache is true: a persist directory for hosting regrounding cache. Ideally to be a persist storage that can be shared in between docker instances. Also please don't reuse grounding cache from OIAD.",
  "hume.cdr_cache_dir": "str or null, optional: When specified, Hume will use the path from inside docker to cache CDRs locally so when new reading requests come as long as it's found in local cache, it won't goto API for fetching it again"
}
```


Please copy the config file to `runtime/config.json`

##### To Run the Hume System

Run Hume with the following command:

```bash
docker run -it -v runtime:/extra docker.io/wmbbn/hume:R2022_03_21 /usr/local/envs/py3-jni/bin/python3 /wm_rootfs/git/Hume/src/python/dart_integration/streaming_processing.py
```

Upon succeessful deployment, any resulting json_ld CAGs will be uploaded back to DART at `DART_upload` and the system will continue to listen for kafka messages until you stop it.


<a id="w4"></a>
### [W4](index.html#w4) Document management + reading + integration/assembly + HMI

The difference between W3, W4 and W5 workflows is transparent to Hume. Please see the documentation for [W3](hume.html#w3) above.

<a id="w5"></a>
### [W5](index.html#w5) Document management + reading + integration/assembly + HMI + BYOD

The difference between W3, W4 and W5 workflows is transparent to Hume. Please see the documentation for [W3](hume.html#w3) above.
