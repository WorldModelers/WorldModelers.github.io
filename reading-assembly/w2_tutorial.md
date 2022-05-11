# Tutorial: Reading and knowledge assembly

In this tutorial, we provide a step-by-step example of running
a machine reading system on a set of sample documents and then running
INDRA assembly on the outputs of the system.

In what follows, we assume that our working base folder is `/data`, that this
folder already exists, and all work is done under this path. This is arbitrary
and can be replaced by another appropriate local path.

This tutorial assumes that Eidos and INDRA World are installed according
to their respective instructions.

## 1. Download input documents

First, we need to prepare a set of input documents to run reading on. Depending
on the reading system(s) used, these can be plain text files or CDR files
containing both the plain text of the document and some metadata. In this
example, we will use a set of 423 documents represented as CDRs, available
publicly on Github. 

```bash
cd /data
git clone https://github.com/twosixlabs-dart/world-modelers-demo-docs.git
```

The documents will now be in the `/data/world-modelers-demo-docs/cdrs` folder.

## 2. Configure the ontology

For simplicity, we assume
that the latest version of the default World Modelers ontology is used
for reading and assembly, which is available [here](https://github.com/WorldModelers/Ontologies/blob/master/CompositionalOntology_metadata.yml). Normally, if using this ontology,
no extra steps are needed, however, here we make its use explicit to better
illustrate how a custom ontology could be used.

We will put the ontology in `/data/ontology.yml`, the following command
doing the download:

```bash
wget https://raw.githubusercontent.com/WorldModelers/Ontologies/master/CompositionalOntology_metadata.yml -O /data/ontology.yml
```

## 3. Run reading on documents

Next, we run Eidos on the input documents. For detailed instructions on setting
up Eidos, see [here](eidos.html#w1-reading-only). Assume that the Eidos repository
is in `/data/eidos`. We will put the Eidos output in the `/data/eidos/output`
folder. To point Eidos to the ontology we downloaded in the last step,
we need to edit `/data/eidos/src/main/resources/eidos.conf`, and change
the line

```
wm_compositional = ${ontologies.path}/CompositionalOntology_metadata.yml
```

to

```yaml
wm_compositional = /data/ontology.yml
```

We can now go to the Eidos repository folder and run Eidos. The last parameter
in the call to Eidos below is the thread count which we set to 4 to allow
Eidos to use 4 threads in parallel.

```bash
cd /data/eidos
mkdir -p output
sbt "runMain org.clulab.wm.eidos.apps.batch.ExtractCdrMetaFromDirectory /data/world-modelers-demo-docs/cdrs /data/eidos/output /data/eidos/times 4"
```

Reading can take a few hours. For faster results, start with an input folder
that only contains a subset of CDRs.

## 4. Process reader outputs and run assembly

After Eidos finished reading, we can process its outputs using INDRA and
run an assembly pipeline with configurable steps. In this example, we will
interact with INDRA World using its native Python environment. We need to
prepare an input file telling INDRA where to source reader output results from.
Below we do this using some simple Python code.

```python
import json
import glob

eidos_outputs = glob.glob('/data/eidos/outputs/*.jsonld')
with open('/data/reader_outputs.json', 'w') as fh:
    json.dump({'eidos': eidos_outputs}, fh, indent=1)
```

Assume we want to put INDRA's assembled output into `/data/indra_output`.
We can now run INDRA World as

```bash
mkdir /data/indra_output
indra_world --reader-output-files /data/reader_outputs.json \
    --ontology-path /data/ontology.yml --output-folder /data/indra_output
```

The output will be a JSON-L file in `/data/indra_output/statements.json`

## 5. Examine/analyze results

At this point, we can examine the assembled output from the documents using
INDRA's Statement objects. Each Statement represents a causal Influence between
two Events.

Let's open up an interactive Python session and take a look at the Statements.

```python
from indra.statements import stmts_from_json_file
stmts = stmts_from_json_file('/data/indra_output/statements.json', format='jsonl')
```
