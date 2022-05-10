---
layout: default
title: Delphi
parent: Qualitative Analysis Toolkit
has_toc: true
nav_order: 2
---
# Table of Contents
- [Table of Contents](#table-of-contents)
- [Delphi](#delphi)
  - [Head nodes](#head-nodes)
  - [Editing an edge](#editing-an-edge)
  - [Interventions](#interventions)
  - [Running locally without the HMI](#running-locally-without-the-HMI)
  - [Further reading](#further-reading)
 
# Delphi

Delphi is a modeling engine that models mechanistic interactions between high-level 'concepts' linked by causal influence relations. The Delphi workflow starts with an analyst providing a causal analysis graph (CAG) that informs Delphi how the concepts influence each other.

During the CAG assembly phase, CauseMos, the human-machine interface (HMI) for Delphi, looks up evidence extracted using machine reading on large-scale corpora that relate each edge's source and target concepts. The HMI presents this information to the analyst for scrutiny. Once the analyst has examined the CAG and made any desired modifications, the HMI conveys the CAG (which includes both the metadata about the influence strength attached to each edge and the overall connectivity structure) to Delphi. Delphi utilizes this information to quantify initial edge strengths and polarities, which serve as a starting point for training a probabilistic forecasting model. While having evidence sentences backing an edge is favorable, that is not a must for Delphi to continue training, and it assigns a default edge strength and polarity in such situations.

A distinctive feature of Delphi is the lack of a requirement for an analyst to set the strength or the polarity of any edge manually. Delphi only consults the information from sentences supplied with the CAG and initializes each edge, and when such information is unavailable, Delphi uses a default. Further, Delphi can work even when the sentences available for an edge do not agree on either the magnitude or the polarity of influence they convey.

Delphi treats each edge weight as a combination of strength and polarity, with the sign of the weight corresponding to the polarity. The weight's magnitude informs Delphi of the size of the change in the target node effected by a change in the source node.

Let us look at an example to clarify how Delphi interprets an edge. Consider an edge from node _(X)_ to node _(Y)_ with strength _-2_, and assume _(X)_ increased by _3_ within a single time step. This results in _(Y)_ changing by _(-2 * 3) = (-6)_ due to the change in _(X)_.

While a CAG is the minimal specification Delphi must receive to build a model, each CAG node should ideally be grounded in indicator time series data to harness the full power of Delphi. The goal of Delphi is to learn a model that could generate predictions that mimic the training data. Delphi cannot accomplish this mission effectively without good quality (quantity and resolution) training data.

When attaching indicators to CAG nodes during the model creation stage of the HMI, specifying the correct minimum and maximum values for each indicator guides Delphi to make better predictions. Delphi does not produce predictions outside the prescribed range for each indicator.

An analyst might not be certain about the CAG they build. Sentences relating a pair of concepts do not always agree. Training data is noisy and incomplete. All these factors contribute to uncertainties in the modeling process.

Delphi starts training from the starting edge strengths and polarities it gleans from sentences and searches for better edge weights to align the predictions with the training data. In doing so, Delphi does not learn a single model with a single set of parameters; instead, it learns a set of models that enable Delphi to capture, quantify, and present the uncertainties in the modeling process in the predictions.

When an analyst issues a projection request, Delphi simulates each model in the set and produces a projected trajectory resulting in multiple projections per request. The HMI summarizes the projections based on time steps and presents the results to the analyst as the uncertainty of the prediction.


## Head nodes

Delphi treats CAG nodes that lack incoming edges, i.e., head nodes differently from other nodes when the analyst specifies a period greater than one and applies a seasonal model. The analyst must supply the accurate seasonality of the time series attached to such CAG nodes as the period for Delphi to model them correctly. If the analyst believes that a CAG node without incoming edges is not seasonal, they could convey it to Delphi by setting its period equal to one.


## Editing an edge

After an analyst sees the prediction results of a trained Delphi model, the HMI provides a feature for the analyst to dispute what Delphi has learned as the strength and polarity for an edge. An analyst must supply the weight and the polarity for this purpose.

When Delphi receives such a request, Delphi honors the analyst's wish and freezes those edges at the weight and polarity assigned by the analyst. Then Delphi goes back to accomplish its mission of generating predictions that resemble the training data by training the model again to learn all the parameters, sans the frozen edges.

Therefore, the analyst should keep in mind that freezing edges initiate a ripple effect where other model parameters could change during the subsequent Delphi training phase accompanied by setting an edge. This could potentially make it seem like (upon visual inspection at least) that freezing edges does not have an effect on the predictions made by Delphi.


## Interventions

When an analyst sets the values of indicators at specific time steps, Delphi honors them and outputs those exact values at those time steps. Such changes propagate to downstream nodes, and their predictions will change accordingly.


## Running locally without the HMI

You must have [Docker](https://www.docker.com) installed.

1. Clone the Delphi git repository: [https://github.com/ml4ai/delphi](https://github.com/ml4ai/delphi).
2. Open a command prompt (a terminal) and navigate into the **data** directory within the Delphi root directory. 
3. Download the Delphi database into the **data** directory by typing `curl -O http://vanga.sista.arizona.edu/delphi_data/delphi.db` in the terminal.
4. In the terminal, navigate into the Delphi root directory.
5. Run the Delphi rest server by typing `docker-compose up --build` in the terminal.
   - This will set up Delphi and run the Delphi REST server on port localhost:8123.
   - When this step is successful, you could access Delphi through its [REST API](https://github.com/uncharted-causemos/docs/blob/f860a5a24db30677ce65a917f3defb330d438933/td-models/api.yml).
   - You could interact with the Delphi REST server by using the following commands executed on another terminal window.
6. Run `curl localhost:8123/status` to check whether the Delphi REST server is running correctly.
   - You should see an output similar to `The Delphi REST API was started on 896fa348cc11 in normal mode at UTC 2022-05-10 02:16:33:026`.
7. To create and train a model run: `curl -X POST http://localhost:8123/create-model -d @<create-model-specification-file-name>.json`
   - The **create model specification json file** should be formatted according to the [REST API Specification](https://github.com/uncharted-causemos/docs/blob/f860a5a24db30677ce65a917f3defb330d438933/td-models/api.yml).
   - [An example create model specification json file](https://github.com/ml4ai/delphi/blob/c101dfd4d98cdec0bae089704949190d33ed1c0c/tests/wm/scripts/3nodes_model.json)
8. To check the model training status run: `curl http://localhost:8123/models/<model-id>/training-progress`
   - The **model id** is specified in the **<create-model-specification-file-name>.json** model specification file used to create the model.
9. To check the model status run: `curl http://localhost:8123/models/<model-id>`
10. To create an experiment run: `curl -X POST http://localhost:8123/models/<model-id>/experiments -d @<create-experiment-specification-file-name>.json`
    - The **create experiment specification json file** should be formatted according to the [REST API Specification](https://github.com/uncharted-causemos/docs/blob/f860a5a24db30677ce65a917f3defb330d438933/td-models/api.yml).
    - This call returns an **experiment id** that you should provide when you are querying about an experiment.
    - [An example create experiment specification json file](https://github.com/ml4ai/delphi/blob/c101dfd4d98cdec0bae089704949190d33ed1c0c/tests/wm/scripts/3nodes_projection.json)
11. To query the status of an experiment or the experiment results run: `curl http://localhost:8123/models/<model-id>/experiments/<experiment-id>`
12. To freeze edge weights as a specific value and polarity run: `curl -X POST http://localhost:8123/models/<model-id>/edit-indicators -d @<edit-edge-specification-file-name>.json`
    - The **edit edge specification json file** should be formatted according to the [REST API Specification](https://github.com/uncharted-causemos/docs/blob/f860a5a24db30677ce65a917f3defb330d438933/td-models/api.yml).
    - [An example edit edges specification json file](https://github.com/ml4ai/delphi/blob/c101dfd4d98cdec0bae089704949190d33ed1c0c/tests/wm/scripts/3nodes_2_edges.json)


## Further reading

A mathematics savvy reader is welcome to read the [Delphi technical document](http://vision.cs.arizona.edu/adarsh/Arizona_Text_to_Model_Procedure.pdf), for in-depth explanations of the mathematics behind the Delphi modeling engine.

Someone familiar with C++ programming language could dive deeper into our implementation of the [open-source codebase of Delphi](https://github.com/ml4ai/delphi).

