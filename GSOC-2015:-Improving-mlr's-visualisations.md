## Improving mlr's visualisations.

**Summary:** Improve and extent mlr's visualisations for data, learned models, and other objects. 

**Description:** 
mlr is a powerful package for general-purpose machine learning in R. Read more details on it here and in its tutorial:
https://github.com/berndbischl/mlr

There are already a number of functions for plotting various objects created by mlr, e.g. for predictions of learners described in the tutorial [here](http://berndbischl.github.io/mlr/tutorial/html/predict/index.html). These functions are mostly based on `ggplot`, although there is integration with [ViperCharts](http://viper.ijs.si/) as well.

This project would improve and extend the existing visualisation functionality. Potential avenues for exploring include (but are not limited to) the following:

* Support for model-specific plots that are tightly integrated with the underlying implementation (for example plotting the network of nodes and weights for a neural network or a tree for a decision tree).
* Support for web-based interactive visualisations (for example through [Shiny](http://shiny.rstudio.com/)).
* Support for comparative visualisation of models (for example the predictions of a model with the parameter of a learner set to one value vs. set to another value with the changed predictions highlighted in a meaningful way).

In order to undertake this project, you should have the following skills:

* Interest in and at least a little bit background knowledge of machine learning / predictive modelling.
* (Advanced) R programming.
* Package development with `devtools`, `testthat`, `roxygen2`.
* Basic git / github skills.
* Being able to cooperate with a larger number of people on a larger software project. This requires skills in software engineering, communication and some diligence.
* Interest and some basic experience with data visualisation, e.g. with the `ggplot2` package.

**Mentor:**

* Lars Kotthoff https://github.com/larskotthoff ([@](mailto:lars.kotthoff {at} insight-centre {dot} org))

* Who else from our team?