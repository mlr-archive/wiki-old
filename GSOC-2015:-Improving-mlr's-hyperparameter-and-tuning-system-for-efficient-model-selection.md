## Improving mlr's hyperparameter and tuning system for efficient model selection.

**Mentors:**

* Bernd Bischl https://github.com/berndbischl ([@](mailto:bernd_bischl {at} gmx {dot} net))
* Michel Lang https://github.com/mllg ([@](mailto:michellang {at} gmail {dot} com))

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

**NOW READ THE GENERAL PROPOSAL GUIDELINES IN THE WIKI TOP LEVEL PAGE** 