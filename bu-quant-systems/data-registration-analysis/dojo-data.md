---
layout: default
title: Registering Data in Dojo
parent: Structured Data
grand_parent: Quantitative Analysis Toolkit
nav_order: 1
---

<a href="https://github.com/dojo-modeling/dojo">
    <img src="../../images/dojo/Dojo_Logo_profile.png" width="200px"/> 
</a>

## Data Registration

 Dojo offers a powerful user-driven data normalization capability through its data registration workflow. This workflow is designed to allow analysts, modelers and other users to curate their own datasets for modeling and analysis. Dojo supports the registration of CSV, Excel File, GeoTiff or NetCDF; once registered, datasets are transformed into _indicators_ that are represented in a canonical parquet format with a well-defined structure. Typical examples of data that might be registered are indicators from the [World Bank](https://data.worldbank.org/), [FAO](http://www.fao.org/statistics/en/), or [ACLED](https://acleddata.com/), however users can bring anything they think will be useful for modeling or other analyses. 

Through this process, Dojo captures metadata about the dataset's provenance as well as descriptors for each of its features in order to transform it into a ready-to-use and well understood format. You can learn more about the data registration process [here](https://www.dojo-modeling.com/data-registration.html).

Normalizing data and model outputs to a consistent Geotemporal format facilitates rapid inter-model comparison and visualization via platforms such as [Uncharted Software's](https://uncharted.software/) Causemos tool.

<p align="center">
    <img src="../../images/dojo/causemos_viz.png" width="400" title="Causemos Modeling Platform"/> 
    <br/>
    <i>Uncharted's Causemos Platform</i>
</p>