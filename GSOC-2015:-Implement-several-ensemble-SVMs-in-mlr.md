
## Implement several ensemble SVMs in mlr

**Summary:** Implement several ensemble SVM learners in mlr and improve mlr to be able to handle ensemble learners in a systematic way.

**Description:** 
Ensemble learning is a powerful method to utilize the diversity of machine learning methods. An ensemble of learners is potentially able to outperform every one of its members. While in general this is well-known, the full power of ensembles, especially in applications, is still not often exploited. One of the reasons for this is that many software packages exhibit none or only rudimentary support for ensemble learning, but no ready-to-use learners.

This is also true for mlr, one of the larger general-purpose machine learning libraries in R (see https://github.com/berndbischl/mlr for more information on mlr). Although mlr contains a variety of machine learning routines and supports basic ensemble methods like boosting and bagging too, and furthermore basic building blocks like clustering and random subspace, mlr includes no ready-to-use ensemble learner. 

Goal of this project is to implement a few ensemble learners. This problem will be approached in a hands-on, step-by-step fashion and will focus solely on ensemble support vector machines (SVM), as these are very promising algorithms to reduce the quadratic complexity of SVMs. Three ensemble SVM learners have been chosen:

* Clustered Support Vector Machines (http://jmlr.org/proceedings/papers/v31/gu13b.html), where the input space is clustered by K-Means and in each cluster an SVM is trained. These local SVMs are regularized by an global SVM. The problem can be reduced to a standard SVM problem and can be solved by any off-the-shelf SVM solver like LIBSVM. 

* Divide-and-Conquer SVM (http://arxiv.org/abs/1311.0914), which is a relatively new approach that seems to provide an order of magnitude of speed-up over standard LIBSVM. Matlab code is provided by the author (see http://www.cs.utexas.edu/~cjhsieh/dcsvm/). 

* Mixture of SVM Experts (see http://dl.acm.org/citation.cfm?id=638957). This is one of the first approaches to ensemble SVMs, where the output of the SVM base learners is fed to a neural network that learns to control the importance of each SVM learner. This is a more general approach, where the SVMs could be replaced by any other base learner. 

By implementing these blocks in mlr, the practical value of mlr will enhance greatly, as it is well-known that Ensemble SVMs are in general more efficient than a single SVM. Potentially they can reduce the sup-quadratic runtime of SVMs to sub-quadratic, making SVMs feasible in practical terms. As none dedicated implementations of ensemble SVMs exist currently, these first steps will pave the road for efficient state-of-the-art SVM implementations in R. 



**Related work:** 
* There are several R packages capable of creating ensemble learners, like h2o (https://github.com/h2oai/h2o/tree/master/R/ensemble), but nearly all of them specialize on specific ensembles only. For a list of these specialized packages see  http://blog.revolutionanalytics.com/2014/04/ensemble-packages-in-r.html . None of them contain any kind of specialized ensemble SVM learner. They only allow for construction of standard ensembles, like bagging or boosting, that do not use the specific properties of SVMs.


**Potential tasks:** 
* Define what is needed for the three ensemble SVMs, e.g. the mixture of experts needs an neural network.

* Implement the above mentioned three ensemble SVM learner as pure R functions.

* Speed-up the ensemble SVM learners by implementing bottlenecks in C++.

* From the gained experience, create additional methods for the creation of ensemble learners in mlr.

The three algorithms are sorted by implementations efforts, i.e. the first one is easy to implement, the second one is more demanding while the third needs the student to understand how different machine learning methods (neural networks and SVMs) can be used to supplement each other. 
We expect that the first task contains some learning of the R language, and can be completed very well within two weeks. The second algorithm has a working matlab-code, which will be very useful to implement it in R. Thus, we expect the task to be easily finished within four weeks. The last task is more demanding and an implementation should be possible also within a month. 


**Skills required:** 

* Background knowledge in machine learning and support vector machines and the interest to implement these in mlr. Having successfully attended to an online course like Andrew Ng's 'Machine Learning' (see https://www.coursera.org/course/ml) is a good basis.  

* R programming

* Package development with devtools, testthat, roxygen2

* Basic git / github skills

* Being able to cooperate with a larger number of people on a larger software project. This requires skills in software engineering, communication and some diligence.


**Expected Results:** 
* Write pseudo-code for the above three methods and identify building blocks (e.g. DC-SVM needs kernel k-means). 

* Implement these in mlr (some exist, some do not). These must be shown to work by themselves on benchmark data sets.

* Identify all hyperparameters of the three methods, what extra paramaters must be set aitionally to the number of ensembles.

* Implementation of all three methods as separate learners in mlr (in the order above). 

* Reproduce the key experimental part in the corresponding papers, i.e. show that the implemented solver exhibits a similar accuracy. Do this also step-by-step, i.e. algorithm by algorithm.

* If time permits: As implementations in R are often slower than in languages like C/C++, try to speed things up by exporting parts of the code to C++. Ideally the implementation should nearly as fast as stated in the corresponding papers.


**Test:**

* Read and understand the cited papers on a practical level. This means that the student can explain how the algorithms work (Deeper understanding of the theory is helpful, but not necessary for the implementation). This should be shown by a pseudo-code version of the algorithms.

* The implemented learners can be applied to a binary classification data set like australian (see LibSVM data set page http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html).

* The implementations are faster than a single SVM on a larger data set like covertype, when the number of ensemble members becomes large enough (if the paper says so).

* If possible, the results from the corresponding papers can be reproduced.


**Mentors:**

* Aydin Demircioglu https://github.com/aydindemircioglu ([@](mailto:aydin.demircioglu {at} ini {dot} rub {dot} de))

* Bernd Bischl https://github.com/berndbischl ([@](mailto:bernd_bischl {at} gmx {dot} net))
