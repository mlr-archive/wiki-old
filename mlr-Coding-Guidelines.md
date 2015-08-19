* Use a proper editor for programming. Like vim, emacs, sublime, RStudio. 

* Read and follow the style guide here. Yes, really. Bernd hates cleaning up such stuff behind others.
  https://github.com/tudo-r/PackagesInfo/wiki/R-Style-Guide

* Every (major) piece of code you add or change must be unit tested.

* What ever you implement, you will document in roxygen. Look at other functions to see how this works. 
Input / Output? What happens in the method? Mention really important details? Like "@family", dislike "@seealso". Sometimes: Should I cite paper? In summary: **Be brief, but precise and helpful to the user!**

* Every longer, more complex operation get commented properly in code. See style guide.

* Every methodical function and method should be explained and quoted.
 * Explain roughly in the documentation so that reading the paper is not necessary for a basic understanding.
 * Quote the paper using roxygen `@references [Author A], [Author B], and [Author C]; [Title: Subtitle], [Journal Volume x] ([Year]), ..., [?Pages]`.

* We like Michel's "dt" tool here. Maybe you like it too? 
  https://github.com/tudo-r/dt

* Before you push you will run at least once at the end
  * The relevant unit tests. Often this is the group "base" with "dt test --filter=base".
  * "R CMD check" or "dt check". No errors, warnings, notes! 

* Your unit tests and R examples will be of perfect compromise of
  * They test / demo everything relevant
  * They run really fast. Maybe in much less then a second. Yes, sometimes difficult, but work on it.

* Do not break travis, before you end your "work cycle". Actually, do not break it at all. Watch the button. The previous hint above should help you in 99% of cases. But: Our unit tests are now quite complex. If you get confused why stuff does not work, ask.

* Every new thing you add, exported signature you change or major behavior you change, gets mentioned in NEWS.
* If you find a bug, always do this: Reproduce via test, THEN repair. Then make sure test runs. Reread the code piece again you touched. Can the structure be improved? If this can be done quickly, do it now.
For more complex stuff: Open up a clearly understandable issue. Best with a minimal and reproducing example. 

* When adding a new plot function that requires more than extracting a part of an existing object and using `reshape`, add a "data generation" function which outputs an object that has an S3 class. For example
`generateLearningCurveData` returns of an object of class `LearningCurveData` (a named list) which can be plotted with `plotLearningCurve`. This allows users to create custom plots easily with the "data generation" functions. Often it makes sense to put "data generation" and plotting functions in the same file, which is usually named, for example "generateLearningCurve.R".







  