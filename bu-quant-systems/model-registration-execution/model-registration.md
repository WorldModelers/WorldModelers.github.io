---
layout: default
title: Model Registration
parent: Registering and Running Expert Domain Models
grand_parent: Bottom Up Quantitative Systems
---

## Model Registration

The model registration workflow is designed to provide domain modelers with a friendly and familiar environment from which to install, setup, and execute their model. Throughout this process, the modeler is queried for key information about model metadata and how to parameterize the model. The modeler also annotates model outputs so that they can be automatically transformed into a ready-to-use and well understood format each time the model is executed. The final step of the model registration workflow is the publication of a working "black box" model Docker container to Dockerhub. These containers can run the model with a set of explicit directives; however the Dojo modeling engine is naive to the inner workings of the model container. 

<p align="center">
    <img src="images/dojo/containerization_environment_medium.png" width="100%" title="Dojo Containerization Environment"/> 
    <br/>
    <i>Dojo Containerization Environment</i>
</p>

Learn more about the model registration process in Dojo [here](https://www.dojo-modeling.com/model-registration.html).