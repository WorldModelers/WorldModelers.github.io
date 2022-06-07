---
title: INDRA World workflows
has_children: false
parent: INDRA World
nav_order: 1
---
## INDRA World Workflows

## Contents
* [Integrated system](#integrated-system)
* [Reading and assembly](#reading-and-assembly)

<a id="integrated-system"></a>
### [Integrated system](index.html#integrated-system)

INDRA World is part of the integrated Causal Relation Extraction and Assembly
Toolkit where it serves as an integrator of reader outputs and incremental
knowledge assembly. In this context, INDRA World is running as a containerized
service and exposes a REST API to communicate with other components.
This REST API is available at http://localhost:9444 by default.

INDRA World also exposes an Assembly Dashboard where you can monitor
(query for) reader outputs that have already been produced for some input
documents, and filter these to define a scope for assembly. Then you can
fill out some details to define and generate a new assembled corpus that
can be loaded into the CauseMos system for interactive exploration.
The dashboard is available at http://localhost:9444/dashboard by default. Here,
you can enter some optional search criteria to find reader output records and
click on "Find reader output records" to get a table of results. Once you
identify an appropriate set, you can fill out the second form on the bottom
with a corpus ID, display name and description, and then click on
Run assembly to produce the results.

Once a corpus is created, it can be loaded into CauseMos. INDRA World's REST
API also allows incrementally assembling new content against an existing
corpus.

<a id="Reading and assembly"></a>
### [Reading and assembly](index.html#reading-and-assembly)

In this workflow INDRA World processes outputs from one or more reading systems
(Eidos, Hume or Sofia) as input. We assume that each reading system was
already run and produced a number of output files. INDRA World assembly can be
done using the [command line interface](https://github.com/indralab/indra_world#command-line-interface)
either natively (if an appropriate Python environment and INDRA World and its
dependencies are installed) or through Docker.

```
indra_world --reader-output-files READER_OUTPUT_FILES --ontology-path ONTOLOGY_PATH --output-folder OUTPUT_FOLDER
```

In the above, `READER_OUTPUT_FILES` refers to a JSON file with the following
structure
```
{
 "eidos":
 [
 "/path/to/file1",
 "/path/to/file2",
 ],
 "hume": [
 ...
 ]
}
```
where keys are reading systems and values are lists of paths to their output
files.

`ONTOLOGY_PATH` is a path to a standard ontology YAML file.
`OUTPUT_FOLDER` refers to a folder in which the resulting `statements.json`
JSON-L dump of assembled INDRA Statements will be written. For more optional
arguments, see the CLI documentation.
