---
title: Reading only tutorial
has_children: false
parent: Corpus Knowledge Extraction and Assembly Toolkit
nav_order: 9
---
# Reading only tutorial
In this example, we provide step-by-step instructions for running the Hume machine reading system on a set of sample documents.

In the steps below, we assume that our working folder is `runtime`, that this folder already exists and all work is done under this path. This is arbitrary and can be replaced by another appropriate local path.

This example assumes that the image for the Hume container has already been downloaded from [Docker hub](https://hub.docker.com/r/wmbbn/hume).

## 1. Download sample documents
As a first step, we need to identify a set of sample documents to use as input. The World Modelers demo set of documents are publicly available on [Github](https://github.com/twosixlabs-dart/world-modelers-demo-docs). The demo document set includes both the raw source documents and the CDR files which contain both the text of the raw documents and some metadata. In this example we'll use the CDRs as input to Hume.

```bash
cd runtime
git clone https://github.com/twosixlabs-dart/world-modelers-demo-docs.git
```

The input documents will now be in the `runtime/world-modelers-demo-docs/cdrs` folder.

## 2. Configure the Ontology
For the purposes of this example, we assume the latest version of [the default World Modelers ontology](https://github.com/WorldModelers/Ontologies/blob/master/CompositionalOntology_metadata.yml) will be used. Normally, if using this ontology, no extra steps are needed, however, here we make its use explicit to better illustrate how a custom ontology could be used.

We will put the ontology in `runtime/ontology.yml`, the following command doing the download:

```
wget https://raw.githubusercontent.com/WorldModelers/Ontologies/master/CompositionalOntology_metadata.yml -O runtime/ontology.yml
```

## 3. Create an output directory
Create an output directory inside the working folder so that it can be accessed by both the local system and the docker instance.

```bash
mkdir runtime/output
```
## 4. Create a Docker config file
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

## 5. Run Hume on the documents
Finally, we run Hume on the input documents. Hume will write its output to the `runtime/output/results/$TIMESTAMP/results` folder, where `$TIMESTAMP` refers to a string representing the date/time of the run.

Note: In the command below, replace the `$RUNTIME` variable with the absolute path of your `runtime` folder (for example `/home/wmuser/runtime`).

```bash
docker run -it -v $RUNTIME:/extra docker.io/wmbbn/hume:R2022_03_21 /usr/local/envs/py3-jni/bin/python3 /wm_rootfs/git/Hume/src/python/dart_integration/manual_processing.py
```

Reading can take a few hours. For faster results, start with an input folder that only contains a subset of CDRs.
