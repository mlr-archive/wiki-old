We use a git “gatekeeper” workflow model, where every code change to the master branch, whether from the main developers or outside contributors, should be a pull request, which is then checked and possibly refined through reviews. How this works in detail is outlined below. If you have questions, feel free to ask in the tracker, we are happy to help.

- Every change to the code **must** be a pull request. Lars, Michel and Bernd have the license to directly push to the master branch and merge PRs. But it is strongly encouraged that they issue pull requests, too. Nobody should merge his own PR.
- Every major change to **mlr’s core system**, i.e., training, resampling, wrappers, etc, should be **reviewed by 2 persons**.
- Here is a minimal check list before pull requests can be merged. Do **not** deviate from this without asking / a proper reason!  
  - Travis passes. But also **always** check the output for NOTES and WARNINGS from the R check.
  - Commits squashed into 1 with a meaningful commit message, see
https://github.com/ginatrapani/todo.txt-android/wiki/Squash-All-Commits-Related-to-a-Single-Issue-into-a-Single-Commit
  - Unit tests added/changed as appropriate. **Every** detected bug, major addition or change must result in a **new, good test**.
  - NEWS: Is it an API / behavior change wrt to the prior version? Then a line must be in **NEWS**.
Code readable, commented and follows [style guide](https://github.com/tudo-r/PackagesInfo/wiki/R-Style-Guide)?
  - Is it an API change? Has the documentation at **all** relevant places been adapted? This includes the tutorial.
  - **The old API cannot be changed so existing client code breaks**. Sometimes such a change is unavoidable and preferable to improve the structure and the exported names of the package. Then use the “deprecate” mechanism explained below. 

## General rules

Read those if you are new to the project.
- Use a proper editor for programming. Like vim, emacs, sublime, RStudio.
- Read and follow the [style guide](https://github.com/tudo-r/PackagesInfo/wiki/R-Style-Guide). Yes, really. Bernd hates cleaning up such stuff behind others.
- Whatever you implement, you will document in roxygen. Look at other functions to see how this works. Input / Output? What happens in the method? Mention really important details? Like "@family", dislike "@seealso". In summary: Be brief, but precise and helpful to the user!
- Every longer, more complex operation get commented properly in code. See style guide.
- Every function that implements functionality described in the literature should be explained and the relevant literature cited.
  - Explain the high-level concept in the documentation so that reading the paper is not necessary for a basic understanding.
  - Cite the paper using roxygen @references [Author A], [Author B], and [Author C]; [Title: Subtitle], [Journal Volume x] ([Year]), ..., [?Pages].
- We like [Michel's "rt" tool](https://github.com/rdatsci/rt) here. Maybe you like it too?
- Before you push you will run at least once at the end
  - The relevant unit tests. Often this is the group "base" with "dt test --filter=base".
  - "R CMD check" or "dt check". No errors, warnings, notes!
- Your unit tests and R examples will be the perfect compromise between
  - They test / demo everything relevant.
  - They run really fast. Maybe in much less then a second. Yes, sometimes difficult, but work on it.
- If you find a bug, always do this: Reproduce via test, THEN repair. Then make sure test runs. Reread the code piece again you touched. Can the structure be improved? If this can be done quickly, do it now. For more complex stuff: Open up a clearly understandable issue. Best with a minimal example that reproduces the bug.
- If you do change the API:
  - Deprecate the old code, use [`.Deprecated()`](https://stat.ethz.ch/R-manual/R-devel/library/base/html/Deprecated.html) at the beginning of the deprecated method. This only outputs a warning, it doesn’t automatically call the new function.
  - Carefully explain in NEWS what you did.