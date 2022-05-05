---
layout: default
title: Sensei
parent: Qualitative Analysis Toolkit
has_toc: true
nav_order: 4
---

# Sensei
`v0.2.4`

[Sensei](https://github.com/dojo-modeling/sensei) is a data-driven top-down modeling engine that provides projections, as well as parameter and uncertainty estimates for time series where variable relationships are defined by a CAG structure. Sensei models the multivariate time series as a set of univariate time series models with "regressors" defined by the CAG structure. That is to say, each node in the CAG gets its own model, which consists of a univariate time series model which parameterizes the trend and seasonality of the time series, as well as coefficients on the incoming edges from one-step-behind values. We compute parameters and projections step-wise, i.e. every model estimates one-time-step-ahead projections iteratively. 

The model we use for univariate time series is the [Damped Local Trend (DLT)](https://uber.github.io/orbit/tutorials/dlt.html) model , variants of which are generally top performers on the [M3 competition](https://www.google.com/search?q=m3+competition+forecasting&ei=a4BEYozsD5GUkwWcka6oBQ&ved=0ahUKEwjMzZKEnO72AhURyqQKHZyIC1UQ4dUDCA4&uact=5&oq=m3+competition+forecasting&gs_lcp=Cgdnd3Mtd2l6EAMyBQgAEIAEMgYIABAWEB46BwgAEEcQsAM6BwgAELADEEM6CggAEOQCELADGAE6FQguEMcBEKMCENQCEMgDELADEEMYAjoPCC4Q1AIQyAMQsAMQQxgCOgQIABBDOggIABCABBDJA0oECEEYAEoECEYYAVD6A1jYEGCaEWgBcAF4AIABT4gBuwaSAQIxMpgBAKABAcgBEsABAdoBBggBEAEYCdoBBggCEAEYCA&sclient=gws-wiz). The parameters and uncertainty are estimated using Maximim A Posteriori (MAP) which offers good accuracy at interactive speed. 
