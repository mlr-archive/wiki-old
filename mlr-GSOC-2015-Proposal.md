a) On this page we will outline our GSOC 2015 project proposal
IF THIS LINE IS HERE THE PROPOSAL IS NOT DONE YET!

b) We are willing to work with students and mentor other projects which deal with
"mlr - Machine Learning in R" if students have a different preference for another topic in machine learning / the software.
**Students then need to approach us soon enough so we can work on such a proposal together.**

## Improving mlr's hyperparameter and tuning system for efficient model selection.

**Summary:** Improve mlr's hyperparamter system with much more "default" knowledge and make hyperparameter tuning more flexible, efficient and convenient. 

**Description:** 
mlr is a powerful package for general-purpose machine learning in R. Read more details on it here and in its tutorial:
https://github.com/berndbischl/mlr

mlr already contains a very powerful parameter description system for machine learning methods, which is based on our ParamHelpers package:

https://github.com/berndbischl/ParamHelpers

You can study how this are used in Learner parameter definition here:

http://berndbischl.github.io/mlr/tutorial/html/create_learner/index.html

and how it is used for tuning here:

http://berndbischl.github.io/mlr/tutorial/html/tune/index.html

But it also has some current drawbacks and options for strong improvements, see the list of tasks below.

**Related work:** 
* Add section from our paper?
* Mention caret tuning?

**Potential tasks:** 
* Defaults of Learner parameters can only be static constants. Allowing for data-dependent functions     would be much better. Eg for and SVM I might want to have the default function
gamma = 1/p, where p is the number of features. 

* Learners should encode whether a parameter can likely affect the predictive performance, the runtime, or is just "technical", e.g. a "verbose" parameter.

* Parameters should know their default box-constraints for optimization. Currently the user has to set these manually for a tuning run.

* Parameters should encode whether it is preferable to optimize them with a transformation, e.g. on a logscale. Eg. for the SVM again, we typically optimize C and gamma on a log2 scale from -15 to 15.

* Using the submodel trick in tuning:
https://github.com/berndbischl/mlr/issues/223


**Skills required:** 

* Interest in and at least a little bit background knowledge of machine learning / predictive modelling

* R programming

* Package development with devtools, testthat, roxygen2

* Basic git / github skills

* Being able to cooperate with a larger number of people on a larger software project. This requires skills in software engineering, communication and some diligence.

**Test:** Fork the package on [GH](https://github.com/berndbischl/mlr) and create a pull-request which implements a new learner. Or work on something simple in our issue tracker.

**Mentor:**

* Bernd Bischl https://github.com/berndbischl ([@](mailto:bernd_bischl {at} gmx {dot} net))

* Who else from our team?


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