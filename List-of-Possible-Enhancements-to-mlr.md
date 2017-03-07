Here is a (surely not complete) list of possible enhancements to mlr which we would like to support in the nearer future. 

We especially welcome others to contribute, so feel free to add your ideas below, including any relevant information about the possible extension and why it may be important for users.  

We also welcome anyone to work on any of the enhancements mentioned on this page. Before you start working on integrating anything below, please open an issue in our [issue tracker](https://github.com/mlr-org/mlr/issues) and let us know, so we can update this page and ensure effort is not duplicated.    

If you are a new developer, please first check out our [coding guidelines](https://github.com/mlr-org/mlr/wiki/mlr-Coding-Guidelines) and [style guide](https://github.com/rdatsci/PackagesInfo/wiki/R-Style-Guide) before working on any of the enhancements below.

# New Learners From Existing R Package

- Check out the tutorial guide for [custom learners](http://mlr-org.github.io/mlr-tutorial/devel/html/create_learner/index.html) for guidance

   |      Number     |   Package     |                                     Method            | Description    |
:--|    :----------:  |   :---------:  |                                     :-----------------:          | :------:   |
1  |        adaptDA   |        amdai   |                         Adaptive Mixture Discriminant Analysis   |            |
2  |            arm   |     bayesglm   |                              Bayesian Generalized Linear Model   |            |
3  |          binda   |        binda   |                                   Binary Discriminant Analysis   |            |
4  |     bnclassify   |         awnb   |                Naive Bayes Classifier with Attribute Weighting   |            |
5  |     bnclassify   |        awtan   | Tree Augmented Naive Bayes Classifier with Attribute Weighting   |            |
6  |     bnclassify   |   nbDiscrete   |                                         Naive Bayes Classifier   |            |
7  |     bnclassify   |     nbSearch   |                           Semi-Naive Structure Learner Wrapper   |            |
8  |     bnclassify   |          tan   |                          Tree Augmented Naive Bayes Classifier   |            |
9  |     bnclassify   |    tanSearch   |Tree Augmented Naive Bayes Classifier Structure Learner Wrapper   |            |
10 |            bst   |        bstLs   |                                           Boosted Linear Model   |            |
11 |            C50   |         C5.0   |                                                           C5.0   |            |
12 |          caret   |          bag   |                                                   Bagged Model   |            |
13 |          caret   |     bagEarth   |                                                    Bagged MARS   |            |
14 |          caret   |      pcaNNet   |                        Neural Networks with Feature Extraction   |            |
15 |        caTools   |   LogitBoost   |                                    Boosted Logistic Regression   |            |
16 |     elasticnet   |         enet   |                                                     Elasticnet   |            |
17 |          enpls   |        enpls   |                      Ensemble Partial Least Squares Regression   |            |
18 |         evtree   |       evtree   |                            Tree Models from Genetic Algorithms   |            |
19 |        fastICA   |          icr   |                               Independent Component Regression   |            |
20 |           foba   |         foba   |                       Ridge Regression with Variable Selection   |            |
21 |            gam   |          gam   |                                    Generalized Additive Models   |            |
22 |           gpls   |         gpls   |                              Generalized Partial Least Squares   |            |
23 |            hda   |          hda   |                          Heteroscedastic discriminant analysis   |            |
24 |      HDclassif   |         hdda   |                         High Dimensional Discriminant Analysis   |            |
25 |        HiDimDA   |         Mlda   |               Maximum Uncertainty Linear Discriminant Analysis   |            |
26 |        HiDimDA   |        RFlda   |                      Factor-Based Linear Discriminant Analysis   |            |
27 |          ipred   |         slda   |                        Stabilized Linear Discriminant Analysis   |            |
28 |          ipred   |    ipredbagg   |                                                    Bagged CART   |            |
29 |        kerndwd   |      kerndwd   |             linear and kernel distance weighted discrimination   |            |
30 |           klaR   |       loclda   |              Localized version of Linear Discriminant Analysis   |            |
31 |           KRLS   |     krlsPoly   |                    Polynomial Kernel Regularized Least Squares   |            |
32 |           KRLS   |         krls   |         Radial Basis Function Kernel Regularized Least Squares   |            |
33 |           laGP   |        newGP   |                                               Gaussian Process   |            |
34 |           lars   |         lars   |                                         Least Angle Regression   |            |
35 |        logicFS   |     logicBag   |                                        Bagged Logic Regression   |            |
36 |         mboost   |     gamboost   |                             Boosted Generalized Additive Model   |            |
37 |          mlegp   |        mlegp   |                                               Gaussian Process   |            |
38 |           mgcv   |          gam   |                       Generalized Additive Model using Splines   |            |
39 |           nnls   |         nnls   |                                     Non-Negative Least Squares   |            |
40 |   oblique.tree   | oblique.tree   |                                                  Oblique Trees   |            |
41 |        partDSA   |      partDSA   |  Partitioning Using Deletion, Substitution, and Addition Moves   |            |
42 |   penalizedLDA   | PenalizedLDA   |                         Penalized Linear Discriminant Analysis   |            |
43 |        plsRcox   |       coxpls   |                                   Cox-Model on PLSR components   |            |
44 |        plsRcox   |      coxpls2   |                                   Cox-Model on PLSR components   |            |
45 |        plsRcox   |      coxpls3   |                                   Cox-Model on PLSR components   |            |
46 |        plsRglm   |      plsRglm   |                Partial Least Squares Generalized Linear Models   |            |
47 |        probFDA   |         pfda   |                    Probabilistic Fisher discriminant analysis    |            |
48 |           qrnn   |         qrnn   |                             Quantile Regression Neural Network   |            |
49 | quantregForest   |          qrf   |                                         Quantile Random Forest   |            |
50 |   randomForest   |        parRF   |                                         Parallel Random Forest   |            |
51 |         relaxo   |       relaxo   |                                                  Relaxed Lasso   |            |
52 |       robustDA   |         rmda   |                           Robust Mixture Discriminant Analysis   |            |
53 |           rocc   |      tr.rocc   |                                           ROC-Based Classifier   |            |
54 |          rrcov   |       QdaCov   |                         Robust Quadratic Discriminant Analysis   |            |
55 |        rrcovHD   |       CSimca   |                                                          SIMCA   |            |
56 |        rrcovHD   |       RSimca   |                                                   Robust SIMCA   |            |
57 |            RRF   |          RRF   |                                      Regularized Random Forest   |            |
58 |            RRF   |    RRFglobal   |                                      Regularized Random Forest   |            |
59 |          RSNNS   |          rbf   |                                  Radial Basis Function Network   |            |
60 |          RSNNS   |       rbfDDA   |                                  Radial Basis Function Network   |            |
61 |          RWeka   |          LMT   |                                           Logistic Model Trees   |            |
62 |          RWeka   |           M5   |                                                     Model Tree   |            |
63 |          RWeka   |      M5Rules   |                                                    Model Rules   |            |
64 |           SDDA   |      sddaLDA   |                 Stepwise Diagonal Linear Discriminant Analysis   |            |
65 |           SDDA   |      sddaQDA   |              Stepwise Diagonal Quadratic Discriminant Analysis   |            |
66 |           sdwd   |         sdwd   |                        Sparse distance weighted discrimination   |            |
67 |            snn   |        mybnn   |                             Bagged Nearest Neighbor Classifier   |            |
68 |            snn   |        myknn   |                                  K Nearest Neighbor Classifier   |            |
69 |            snn   |       myownn   |                   Optimal Weighted Nearest Neighbor Classifier   |            |
70 |            snn   |        mysnn   |                         Stabilized Nearest Neighbor Classifier   |            |
71 |            snn   |        mywnn   |                           Weighted Nearest Neighbor Classifier   |            |
72 |      sparseLDA   |    sparseLDA   |                            Sparse Linear Discriminant Analysis   |            |
73 |           spls   |         spls   |                                   Sparse Partial Least Squares   |            |
74 |          stats   |          ppr   |                                  Projection Pursuit Regression   |            |
75 |        superpc   |      superpc   |                        Supervised Principal Component Analysis   |            |
76 |      sparsenet   |    sparsenet   |           Sparse linear regression with nonconvex optimization   |            |
77 |           sprm   |         prms   |                                    Partial robust M regression   |            |
78 |           sprm   |        sprms   |                             Sparse partial robust M regression   |            |
79 |           sprm   |        prmda   |                           Robust PLS for binary classification   |            |
80 |           sprm   |       sprmda   |                Sparse and robust PLS for binary classification   |            |
81 |           vbmp   |   vbmpRadial   |             Variational Bayesian Multinomial Probit Regression   |            |                    

# Speculative Enhancements

- These are ideas from the mlr community

 Number |      Idea     |   Ref Issue    |
:--|    :----------:  |:----------:
1 | Making a super learner from base learners applied to different parts of the data | [#153](https://github.com/mlr-org/mlr/issues/153)
2 | Sparse matrix support | [#453](https://github.com/mlr-org/mlr/issues/471)
3 | Score output for classes | [#355](https://github.com/mlr-org/mlr/issues/355)
4 | Smote for multiclass problems | [#905](https://github.com/mlr-org/mlr/issues/905)
5 | Impute wrappers for established packages | [#156](https://github.com/mlr-org/mlr/issues/156)
6 | Subsampling ensemble variance estimator | [#740](https://github.com/mlr-org/mlr/issues/740)
7 | Ordinal classification | [#852](https://github.com/mlr-org/mlr/issues/852)
8 | makeBaggingWrapper for survival tasks | [#877](https://github.com/mlr-org/mlr/issues/877)
9 | Unified logging | [#544](https://github.com/mlr-org/mlr/issues/544)
10 | Feature selection for clustering | [#541](https://github.com/mlr-org/mlr/issues/541)
11 | Confidence intervals in prediction | [#843](https://github.com/mlr-org/mlr/issues/843)
12 | Allow general model formulas | [#564](https://github.com/mlr-org/mlr/issues/564)
13 | Parallelization of underlying model fit | None
14 | Stability selection | None
15 | Method to create polynomial features | [#645](https://github.com/mlr-org/mlr/issues/645)
16 | Calibration and calibration slope | [#842](https://github.com/mlr-org/mlr/issues/842)
17 | Allow more stopping criteria for feature wrapper | [#104](https://github.com/mlr-org/mlr/issues/104)
18 | Use criterion function for feature selection | [#666](https://github.com/mlr-org/mlr/issues/666)
19 | Allow mandatory covariates during filtering/feature selection | [#170](https://github.com/mlr-org/mlr/issues/170)
20 | Submodel approaches | [#298](https://github.com/mlr-org/mlr/issues/298)
21 | Imbalanced and cost sensitive multiclass modeling | [#821](https://github.com/mlr-org/mlr/issues/821)
22 | Interaction detection methods | None
23 | Plotting undirected graph | None
24 | Plotting bar chart | None