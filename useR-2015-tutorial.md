# useR 2015 Tutorial

**Applied Machine Learning and Efficient Model Selection with mlr**

by Bernd Bischl, Michel Lang

to be held on [useR 2015](http://user2015.math.aau.dk/) in Aarlborg, DK, June 30th, 2015.

Background knowledge required: Basic knowledge of R and machine learning

Potential attendees: Anybody from academia or industry with an interest in modern machine learning

## Brief description of the tutorial

R does not define a standardized interface for all its machine learning algorithms. Therefore, for
any non-trivial experiments you need to write lengthy, tedious and error-prone wrappers to call the
different algorithms and unify their respective output. The mlr package offers a clean, easy-to-use
and flexible domain specific language for machine learning experiments in R. It supports
classification, regression, clustering and survival analysis and connects to nearly a hundred
predictive modeling techniques. The package allows for different hyperparameter optimization and
configuration techniques, including iterated F-racing and sequential model based optimization.
Variable selection is possible through various filter and wrapper approaches. 

Hence, mlr allows data analysts who are neither experts in machine learning nor seasoned
R programmers to nevertheless specify and complex machine learning experiments in short, succinct
and scalable code. Experienced programmers, on the other hand, get to wield a large, well-designed toolbox, 
which they can customize and extend to quickly construct their own algorithms.

The course will enable the participants to understand and apply the basic mlr operations for data
handling and preprocessing, model building, evaluation and resampling. After these basics are
covered we will especially focus on the important aspects of benchmarking, model selection and
hyperparameter tuning. As all of these usually require a large amount of computational resources in
realistic applications, we will show how to easily parallelize them in common parallel environments.
The course will end with a short demonstration on how to access the new OpenML server for open
machine learning (http://www.openml.org) which provides a large repository of benchmark data sets 
and enables reproducible experiments and meta analysis.


## Detailed Outline
* Very brief intro to applied machine learning
* Data handling and machine learning tasks 
* Classification, regression, clustering and survival modeling with mlr
* Performance evaluation and resampling
* Visual model analysis
* Parallelization and high-performance computing
* Model selection and hyper-parameter tuning
* Interfacing the OpenML server with mlr

# Hands on

* Create a classification task for the  Ionosphere data set (package mlbench).
* Remove constant features from the data set.
* Evaluate a random forest on this task. Tune the parameters `mtry` and `nodesize` (both from 1 to 10)
  using a 3-fold cross validation and the random search (see `?makeTuneControlRandom`).
  Set the budget via `maxit` to 20.
* Compare the mean misclassification error (mmce) with the results of single classification tree from the rpart package.
* NB: This is NOT really a proper evaluation of the tuned algorithm. But we have not learned nested CV so far :(
