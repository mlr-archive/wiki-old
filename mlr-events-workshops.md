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

## Install instructions
Install the CRAN version of the package and some optional dependencies which are required for this tutorial:
```{r}
install.packages(c("glmnet", "gridExtra", "ggplot2", "ggvis", "kknn", 
  "irace", "kernlab", "KMsurv", "mlbench", "mda", "mlr", "party", 
  "randomForest", "randomForestSRC", "shiny", "sROC", "devtools", 
  "survMisc", "BatchJobs", "e1071", "rjson"))
```

## Slides and supplementary material
You can find everything [here](https://github.com/mlr-org/user2015_tutorial).

## Hands on

* Create a classification task for the  Ionosphere data set (package mlbench).
* Remove constant features from the data set.
* Evaluate a random forest on this task. Tune the parameters `mtry` and `nodesize` (both from 1 to 10)
  using a 3-fold cross validation and the random search (see `?makeTuneControlRandom`).
  Set the budget via `maxit` to 20.
* Compare the mean misclassification error (mmce) with the results of single classification tree from the rpart package.
* NB: This is NOT really a proper evaluation of the tuned algorithm. But we have not learned nested CV so far :(

# Palermo workshop

Some stuff from Palermo I am too lazy to translate

Vorschlag: mlrLearners paket machen

+ schneller Testen auf Travis
+ wir bleiben nur bei einem extra Paket
+ logisch besser aufgebaut
+ Verwaltbarkeit wird einfacher (log history)

o mini: 1 Learner pro Type (eher Top 10)
o List Learners sollte unabhängig funktionieren
o ideales Testsystem bräuchte 
o option für Paket Autoinstall bei paket installieren. Fehlermeldung zeigt hinweis, wie man es auto installiert

- grundstruktur änderungen müssten umständlich synchronisiert werden
- höhere maintanance
- PRs könnten über beide Pakete gehen


learner property "recommended"

learner ontology

datatable gegen dplyr? 
plyr rauswerfen

printer für chains von wrapper machen

prediction objekte reviewn

plotModel methode für schönsten plot


top10 workhop

- alle im gleichen hotel und arbeitsort super nah 
- raum offen wann wir wollen
- schedule online. mit essen.
- wasser klopapier und gesunde snacks im raum
- bessere vorher teams bilden? noch bessere inhaltliche planung
- ort leichter zu erreichen (flug, anreise)
- mehr funding vorher
  workshop gebühren einnehmren und ummünzen?
- mehrerere räume, ruhig, runde tische mit platz, beamer
- package release vor workshop 

# mlr Warsaw 2018

## Workshop documentation
* [Talk](https://github.com/mlr-org/mlr-outreach/raw/master/2018_04_Warsaw/talk.pdf)
* [Demo](https://github.com/mlr-org/mlr-outreach/raw/master/2018_04_Warsaw/demo.R)
* [Data set](https://github.com/mlr-org/mlr-outreach/raw/master/2018_04_Warsaw/data.rda)

## Further links
* [Link to GitHub](https://github.com/mlr-org/mlr)
* [mlr cheatsheet](https://github.com/mlr-org/mlr-tutorial/raw/gh-pages/cheatsheet/MlrCheatsheet.pdf)
* [Detailed Tutoiral](https://mlr-org.github.io/mlr/)

# mlr @ WhyR?2018 conference

* [Link to Blogpost](http://mlr-org.github.io/whyr-conference)
* [Link to Talks](https://github.com/mlr-org/mlr-outreach/tree/master/2018_07_wroclaw)