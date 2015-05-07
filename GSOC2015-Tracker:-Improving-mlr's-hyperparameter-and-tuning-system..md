# Tracker of the progress for the Hyperparameter and Tuning Project (GSOC 2015)

## Open Issues

Here's a list of open issues, which are somehow related to hyperparameters, tuning, etc.

1. [Issue #279:](https://github.com/berndbischl/mlr/issues/279)

  **Hyperparameter tuning should be more flexible wrt. the number of digits of hyperparameter boundaries (e.g. problem if** ```lower = 1e-5``` **and** ```upper = 1e-4```**, because** ```digit = 4```**).**
 
  Suggested solution:

  * allow user to modify digits in ```convertParamSetToIrace``` (by forwarding such an argument)


1. [Issue #267:](https://github.com/berndbischl/mlr/issues/267)

  **Collect problems, where parameters depend on hyperparameters.**

  Planned approach:

  * keep watching ...

1. [Issue #246:](https://github.com/berndbischl/mlr/issues/246)
  
  **Bug in** ```selectFeatures```**, in case of combination of** ```method = "sfs"``` **and** ```tune.threshold = TRUE```.**

  Planned approach:

  * Bernd assigned the issue to himself

1. [Issue #245:](https://github.com/berndbischl/mlr/issues/245)

  ```analyzeFeatselResult``` **throws an error; the function** ```analyzeFeatselResult``` **tries to convert** ```res$opt.path``` **(with** ```res``` **being the featsel-result) into a** ```data.frame``` **- which does not work.**

  Suggested solution:

  * check, which is the correct element storing the optimization path and correct the function accordingly

1. [Issue #242:](https://github.com/berndbischl/mlr/issues/242)

  **The names of the inner loop of a nested tuning contain the prefix** ```"threshold."```**, which causes an error within the outer loop.**

  Suggested solution:
    1. remove that prefix (i.e. don't even generate it)
    1. look for that prefix in the outer loop and remove it there

1. [Issue #240:](https://github.com/berndbischl/mlr/issues/240)

  **Check infeasible settings of a learner, e.g.** ```makeLearner("classif.svm", type="C-classification", nu=2)```**.**

  Question:
    * Is this issue that important? The parameter ```nu``` will just be ignored - like in the original function ```e1071::svm``` as well. However, if it is important, one could think about making dependency checks, i.e. in case ```nu``` is defined, check whether ```type``` is ```nu-...```

1. [Issue #223:](https://github.com/berndbischl/mlr/issues/223)

  **Submodel issue.**

  First approach towards a solution:
  * check ALL learners to see, where this might be doable

  Question:
  * Should the user be somehow informed that (s)he might want to define a high value for that parameter and advice him/her to afterwards employ the submodel trick for finding the proper parameter setting?!

1. [Issue #207:](https://github.com/berndbischl/mlr/issues/207)

  **data dependent defaults (cf. first item of GSOC proposal)**

  Suggested solution:
  * write a function ```updateLearner```, which takes a learner and a ```task``` / ```data.frame``` and uses those to update data dependent parameters

  Question:
  * Should those parameters be explicitly listed in \texttt{updateLearner} or do you prefer, if the method just "knows", which parameters should be defined (and overwritten)?

1. [Issue #202:](https://github.com/berndbischl/mlr/issues/202)

  **Tune the impute wrapper.**

  Question:
  * Does that mean, we are looking for something, which uses different imputation techniques and tells you, which one works best?!


***

## (hopefully) rather "low-hanging fruits"

The following items should be promptly solvable:

* [item 1 / issue #279](https://github.com/berndbischl/mlr/issues/279): digit issue 
* [item 4 / issue #245](https://github.com/berndbischl/mlr/issues/245): get ```optPath``` within ```analyzeFeatselResult```
* [item 5 / issue #242](https://github.com/berndbischl/mlr/issues/242): naming issue in case of nested tuning

***

## Important issues / Milestones wrt GSOC project

The two items below are very important issues and thus, were also part of the GSOC proposal:

  * [item 9 / issue #223](https://github.com/berndbischl/mlr/issues/223): submodel issue
  * [item 10 / issue #207](https://github.com/berndbischl/mlr/issues/207): data dependent defaults

***

### Planned projects according to GSOC proposal

1. **The current implementation of the learners does not allow dynamic parameters.**

  This problem needs to be solved quickly as the performance of a learner heavily relies on reasonable parameter configurations. Such a 'reasonable' configuration should consider different aspects of a task, such as the number of features and observations of the underlying data set.

  As the implementation of task-dependent information requires the presence of a task, this will influence the current implementation of learners and thus the entire modeling approach of mlr -- due to a possibly new argument 'task'. This problem might increase when considering the fact that some learners should still be able to work without that additional information. Thus, instead of adding 'task' as a new argument, I plan to implement a wrapper, which allows to compute task-dependent parameters and adds them to an existing learner.
  * [*see issue 207*](https://github.com/berndbischl/mlr/issues/207)

2. **As the majority of learners already include (default) information on the box constraints of its parameters, that information should be automatically used when tuning the models -- except if the user manually requests to change the defaults.**

  This step actually requires to create a default parameter set for tuning, based on a given learner. Therefore, I plan to write a function (e.g. called ```makeParamFromLearner```) which creates a parameter set, based on the box constraints of the learner's parameters.
  * *will be processed at a later stage of the GSOC*

3. **Along with the box constraint information, a learner should also provide information on the preferred transformation for each parameter.**

  This task actually requires the addition of a ```transformation``` argument within the ```makeLearner``` function. I will also check, whether it might be useful to actually learn the (reasonable) transformation. Assuming the lower bound of a parameter is ```.125``` (= ```2^(-3)```) and the upper bound ```1024``` (= ```2^10```), it is very likely more reasonable to consider a power-transformation than the identity function.
  * *will be processed at a later stage of the GSOC*

4. **The implemented learners should inform their users which parameters affect the performance of a model (and if possible in which degree)**

  This information could be evaluated in a two-step approach:
    1. Pure 'technical' parameters should be identified by the user that is implementing the new learner. For the existing learners, I will check, which parameters are just 'technical' and which ones actually affect the performance.
    2. In a second step, I suggest to benchmark the effect of parameter configurations on the performance. As those configurations will very likely be task-dependent, I would write a function that allows to benchmark the parameter influence based on the learner and task. 

      In a first approach, that benchmark-function should analyze, how the performance changes, when only a single parameter of the learner (compared to the default settings) is changed. However, as the performance will very likely also be influenced by interactions between parameter configurations, I will also try to implement an interaction-influence-check as well - if the time permits that.

  * *will be processed at a later stage of the GSOC*

5. **As a last major project, I aim to provide access to submodels of a (trained) model.**

  For instance, if one trains a random forest with 500 trees, one should also be able to evaluate random forests consisting of 1 to 499 trees as well, without explicitly training them again, as they have already been created.
  I plan to implement a function that allows to extract those submodels based on a given model and a list of corresponding arguments, e.g. ```getSubmodel(model = rf_model, pars = list(n_tree = 250L))```.
  * [*see issue 223*](https://github.com/berndbischl/mlr/issues/223)
