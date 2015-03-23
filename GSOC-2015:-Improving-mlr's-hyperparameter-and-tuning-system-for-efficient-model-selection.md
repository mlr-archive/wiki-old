## Improving mlr's hyperparameter and tuning system for efficient model selection.

**Mentors:**

* Bernd Bischl https://github.com/berndbischl, melange ID berndbischl ([@](mailto:bernd_bischl {at} gmx {dot} net))
* Michel Lang https://github.com/mllg ([@](mailto:michellang {at} gmail {dot} com)) (Melange ID: mllg)

**Summary:** Enrich mlr's hyperparamter system with a-priori knowledge to make hyperparameter tuning more flexible, efficient and convenient. 

**Description:** 
[mlr](https://github.com/berndbischl/mlr) is a powerful package for general-purpose machine learning in R.
It already contains a very powerful parameter description system for machine learning methods which is based on the [ParamHelpers](https://github.com/berndbischl/ParamHelpers) package.
ParamHelpers is used for the definition of learner parameters as well as parameter tuning, more information is provided by the tutorial pages on [learners](http://berndbischl.github.io/mlr/tutorial/html/create_learner/) and [tuning](http://berndbischl.github.io/mlr/tutorial/html/tune/), respectively.
The current implementation also has some drawbacks and options for strong improvements, see the list of tasks below.

**Related work:** 
The [caret](http://topepo.github.io/caret/index.html) package (arguably the only reasonable comprehensive alternative to mlr) already provides some meta information for some parameters of some learners, i.e. which parameters are should be considered for tuning using which static box constraints. But data dependent defaults and constraints are not possible. Furthermore, caret provides much less powerful tuning algorithms and a less worked out object oriented system for parameters and learners in the background. Also, parameters of combined methods, e.g. preprocessing and modelling, cannot be tuned jointly.

**Potential tasks:** 
* Defaults of Learner parameters can only be static constants. Allowing for data-dependent functions would be much more flexible. E.g., for an SVM I might want to have the default function gamma = 1/p, where p is the number of features. 

* Learners should encode whether a parameter can likely affect the predictive performance, the runtime, or is just "technical", e.g. a "verbose" parameter.

* Parameters should know their default box-constraints for optimization. Currently the user has to set these manually for a tuning run.

* Parameters should encode whether it is preferable to optimize them with a transformation, e.g. on a logscale. Eg., for the SVM again, we typically optimize C and gamma on a log2 scale from -15 to 15.

* Using the submodel trick in tuning:
https://github.com/berndbischl/mlr/issues/223

**Skills required:**
Good knowledge of machine learning, R package development and R in general.

**Test**: Implement a new learner, including its most important hyperparameters. If you are unsure which learner to implement, you can compare the list of [mlr learners](http://berndbischl.github.io/mlr/tutorial/html/integrated_learners/index.html) with the list of [caret learners](http://topepo.github.io/caret/modelList.html) or the CRAN [task view on machine learning](http://cran.r-project.org/web/views/MachineLearning.html).