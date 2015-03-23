## Improving mlr's visualisations.

**Summary:** Improve and extent mlr's visualisations for data, learned models, and other objects. 

**Description:** 
mlr is a powerful package for general-purpose machine learning in R. Read more details on it here and in its tutorial:
https://github.com/berndbischl/mlr

There are already a number of functions for plotting various objects created by mlr, e.g., for predictions of learners described in the tutorial [here](http://berndbischl.github.io/mlr/tutorial/html/predict/index.html#visualizing-the-prediction). These functions are mostly based on `ggplot`, although there is integration with [ViperCharts](http://viper.ijs.si/) as well.

This project aims to extend mlr's visualisation capabilities. This will facilitate a number of things that are beneficial to the community:

- Model analysis. Being able to visually inspect a model and compare it to other models facilitates the understanding of what the learner does internally.
- Teaching. mlr's visualisation capabilities are used for teaching machine learning algorithms and concepts already, but the functionality that is provided at the moment does not go far enough (in particular with respect to visualising models themselves).
- Industrial applications. There is a growing trend for interactive web-based visualisations. R has several packages (e.g. [shiny](http://shiny.rstudio.com)) that facilitate this, but only basic integration with [ViperCharts](http://viper.ijs.si) is currently available in mlr.

**Related Work:**

Many learners provide some functionality to draw predictions or visualise the models, e.g., `plot.lm` (diagnostic plots for linear models) and `plot.nn` (visualization of a fitted neural network). `ggplot` provides a *lot* of drawing and plotting functionality, some of which is already used by mlr. `shiny` provides a way to do more interactive visualisations and is currently not integrated with mlr.

There are a number of other R packages that provide a common interface to different machine learning algorithms (e.g. `caret`), but none of them has extensive visualisation capabilities.

**Potential Tasks:**

This project would improve and extend the existing visualisation functionality. Potential avenues for exploring include (but are not limited to) the following:

* Support for model-specific plots that are tightly integrated with the underlying implementation (for example plotting the network of nodes and weights for a neural network or a tree for a decision tree).
* Support for web-based interactive visualisations (for example through [Shiny](http://shiny.rstudio.com/)).
* Support for comparative visualisation of models (for example the predictions of a model with the parameter of a learner set to one value vs. set to another value with the changed predictions highlighted in a meaningful way).

Each of these directions could be implemented satisfactorily in less than 1 month by someone experienced with R programming, visualisation, and the mlr code base. A total of 3 months allows students to become familiar with mlr and visualisation concepts and exceed the requirements.

**Skills required:**

In order to undertake this project, you should have the following skills:

* Interest in and at least a little bit background knowledge of machine learning / predictive modelling.
* (Advanced) R programming.
* Package development with `devtools`, `testthat`, `roxygen2`.
* Basic git / github skills.
* Being able to cooperate with a larger number of people on a larger software project. This requires skills in software engineering, communication and some diligence.
* Interest and some basic experience with data visualisation, e.g. with the `ggplot2` package.

**Test:**

Resolve [Issue #247](https://github.com/berndbischl/mlr/issues/247).

**Mentors:**

* Lars Kotthoff https://github.com/larskotthoff, melange ID larskotthoff ([@](mailto:lars.kotthoff {at} insight-centre {dot} org))

* Julia Schiffner https://github.com/schiffner, melange ID schiffner ([@](mailto:schiffner {at} math {dot} uni-duesseldorf {dot} de))

* Bernd Bischl can co-mentor for general guidance and technical issues, or more if his tuning project is not selected. https://github.com/berndbischl, melange ID berndbischl ([@](mailto:bernd_bischl {at} gmx {dot} net))
