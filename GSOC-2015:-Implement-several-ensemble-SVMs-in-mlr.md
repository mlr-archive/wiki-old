
## Implement several ensemble SVMs in mlr

**Summary:** Implement several ensemble SVM learners in mlr and improve mlr to be able to handle ensemble learners in a systematic way.

**Description:** 
Ensemble learning is a powerful method to utilize the diversity of machine learning methods. An ensemble of learners is potentially able to outperform every one of its members. While in general this is well-known, the full power of ensembles, especially in applications, is still not often exploited. One of the reasons for this is that many software packages exhibit none or only rudimentary support for ensemble learning, but no ready-to-use learners.

This is also true for mlr, one of the larger general-purpose machine learning libraries in R (see https://github.com/berndbischl/mlr for more information on mlr). Although mlr contains a variety of machine learning routines and supports basic ensemble methods like boosting and bagging too, and furthermore basic building blocks like clustering and random subspace, mlr includes no ready-to-use ensemble learner. 

Goal of this project is to implement a few ensemble learners. This problem will be approached in a hands-on, step-by-step fashion and will focus solely on ensemble support vector machines (SVM), as these are very promising algorithms to reduce the quadratic complexity of SVMs. Three ensemble SVM learners have been chosen:

* Clustered Support Vector Machines (http://jmlr.org/proceedings/papers/v31/gu13b.html), where the input space is clustered by K-Means and in each cluster an SVM is trained. These local SVMs are regularized by a global SVM. The problem can be reduced to a standard SVM problem and can be solved by any off-the-shelf SVM solver like LIBSVM. 

* Divide-and-Conquer SVM (http://arxiv.org/abs/1311.0914), which is a relatively new approach that seems to provide an order of magnitude of speed-up over standard LIBSVM. Matlab code is provided by the author (see http://www.cs.utexas.edu/~cjhsieh/dcsvm/). 

* Mixture of SVM Experts (see http://dl.acm.org/citation.cfm?id=638957). This is one of the first approaches to ensemble SVMs, where the output of the SVM base learners is fed to a neural network that learns to control the importance of each SVM learner. This is a more general approach, where the SVMs could be replaced by any other base learner. 

By implementing these blocks in mlr, the practical value of mlr will enhance greatly, as it is well-known that Ensemble SVMs are in general more efficient than a single SVM. Potentially they can reduce the sup-quadratic runtime of SVMs to sub-quadratic, making SVMs feasible in practical terms. As none dedicated implementations of ensemble SVMs exist currently, these first steps will pave the road for efficient state-of-the-art SVM implementations in R. 



**Related work:** 
* There are several R packages capable of creating ensemble learners, like h2o (https://github.com/h2oai/h2o/tree/master/R/ensemble), but nearly all of them specialize on specific ensembles only. For a list of these specialized packages see  http://blog.revolutionanalytics.com/2014/04/ensemble-packages-in-r.html . None of them contain any kind of specialized ensemble SVM learner. They only allow for construction of standard ensembles, like bagging or boosting, that do not use the specific properties of SVMs.


**Potential tasks:** 
* Understand the three ensemble SVMs and define what is needed for an implementation, e.g. the mixture of experts needs an neural network.

* Implement the above mentioned three ensemble SVM learner as pure R functions.

* Speed-up the ensemble SVM learners by implementing bottlenecks in C++.

* From the gained experience, create additional methods for the creation of ensemble learners in mlr.

* If time permits: As implementations in R are often slower than in languages like C/C++, try to speed things up by exporting parts of the code to C++. Ideally the implementation should nearly as fast as stated in the corresponding papers.


The three algorithms are sorted by implementations efforts, i.e. the first one is easy to implement, the second one is more demanding while the third needs the student to understand how different machine learning methods (neural networks and SVMs) can be used to supplement each other. 
We expect that the first task contains some learning of the R language, and can be completed very well within two weeks by a student. The authors of the second algorithm provided some matlab-code, which will be very useful to implement it in R. Thus, we expect the task to be doable for a student within four weeks. The last task is slightly more demanding, but as the main building blocks (SVMs and neural networks) already exist, implementation will be possible also within a month. 


**Skills required:** 

* Background knowledge in machine learning and support vector machines and the interest to implement these in mlr. Having successfully attended to an online course like Andrew Ng's 'Machine Learning' (see https://www.coursera.org/course/ml) is a good basis.  

* R programming

* Package development with devtools, testthat, roxygen2

* Basic git / github skills

* Being able to cooperate with a larger number of people on a larger software project. This requires skills in software engineering, communication and some diligence.




**Test:**

Create a simple learner that uses kernelized SVM and $K$-Means for binary classification. This is not a 'true' ensemble, but instead a local learner, which could be easily enhanced to a 'true' ensemble. Proceed like this: 

* The learner with use three parameters: $C$, the regularization parameter for the SVM, $\gamma$, the RBF kernel parameter and $n$ the number of clusters. 

* Write a corresponding trainer. The trainer should work with a given binary, labeled dataset as follows: Use  $K$-Means to cluster the training data into $n$ clusters. On each cluster, train an SVM. Assign the trained model with the cluster it was trained on. 

* Write a prediction method. Prediction works by simply determining for a given test point the cluster it belongs to. Then apply the associated SVM model to the test point and return the label the SVM predicted.

It is nice to create this local learner directly in mlr, e.g. as a learner with the name "local.SVM", but not strictly necessary. To show your interest and ability, it is enough to write your own simple routines that use mlr in the background. (Of course, making this directly in mlr will be better.) Test your program with a simple binary data set of your choice with at least 500 data points, which can be obtained e.g. from the LibSVM data set page http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html.


**Mentors:**

* Aydin Demircioglu https://github.com/aydindemircioglu ([@](mailto:aydin.demircioglu {at} ini {dot} rub {dot} de))

* Bernd Bischl https://github.com/berndbischl ([@](mailto:bernd_bischl {at} gmx {dot} net))

