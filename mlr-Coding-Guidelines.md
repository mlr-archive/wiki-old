We use a git “gatekeeper” workflow model, where every code change to the master branch, whether from the main developers or outside contributors, should be a pull request, which is then checked and possibly refined through reviews. How this works in detail is outlined below. If you have questions, feel free to ask in the tracker, we are happy to help.

- Every change to the code **must** be a pull request. Lars, Michel and Bernd have the license to directly push to the master branch and merge PRs. But it is strongly encouraged that they issue pull requests, too. Nobody should merge his own PR. Before you issue or update the pull request, please rebase onto master.
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
- After merging a pull request, **rerun the latest [mlr tutorial build](https://travis-ci.org/mlr-org/mlr-tutorial)**. Unfortunately there's no sensible way to automate this at the moment, so please trigger the build manually to make sure that the tutorial wasn't broken by the change.

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

Setup & Contribution Guidelines
=========

Read this if you are really new to software development in general.

Did you find a bug? Is your favourite learner missing and you want to add it? Or do you have another idea for making mlr better? We welcome all contributions to mlr. While modifying or extending such a large project can seem daunting at first, here are some guidelines on how to get started.

## Version control setup

We assume that git is already installed on your local machine, if not follow [these guidelines](https://help.github.com/articles/set-up-git/). 

Use `git clone` to clone this repo to your local machine:
```
git clone https://github.com/mlr-org/mlr.git
```
<br>
`cd` into cloned repo:
```
cd mlr
```

You should have R set up on your local machine. mlr uses quite a number of other packages (in particular, a large number of packages that provide learners). To extend mlr, you don't need all of them, but it may nevertheless help to install mlr from CRAN with all dependencies and "suggests" packages.

If you're using [RStudio](http://www.rstudio.com/products/rstudio/), you can import mlr as a project by clicking on file -> New Project -> Existing Directory (Browse the mlr project).

### Forking

If you want to make changes to the mlr code that you want to make public or submit back to us, you should
fork the main repository to your account, using the **Fork** button on the top right corner.

Use `git clone` to clone your forked repo to your local machine:
(replace 'your_username' with your github username)
```
git clone https://github.com/your_username/mlr.git
```
<br>
`cd` into cloned repo:
```
cd mlr
```
<br>
Set the `upstream` to mlr parent repo:

The easiest way is to use the https url:
```
git remote add upstream https://github.com/mlr-org/mlr.git
```

or if you have ssh set up you can use that url instead:
```
git remote add upstream git://github.com/mlr-org/mlr.git
```

### Branching

When you develop a new feature, it is recommended to create a new branch for it. Don't modify the *master* branch directly to make the provenance of any new code/feature clear.
```
git branch new_branch
```

When committing changes to the code, please provide meaningful commit messages that let other people know what you've done. If the commit is linked to an issue, provide the number of the issue in the message.

Once you're happy with your changes, you may want to pull in the latest changes from the *master* branch.
Move to the *master* branch, fetch the upstream changes and merge.
```
git checkout master
git fetch upstream
git merge upstream/master
```

Then change back to your new branch and rebase your changes.
```
git checkout new_branch
git rebase master
```
Now all your changes on your current branch will be based on top of the changes in *master* branch.

## Contributing

Once you're happy with your code, please open a [pull request for the main repository](https://github.com/mlr-org/mlr/pulls). This will automatically run [Travis CI](https://travis-ci.org/mlr-org/mlr) on your changes to see if it still builds and all the tests pass. The developer team will get notified automatically of your pull request.

For more information on how to implement code for mlr, please see the [coding guidelines](https://github.com/mlr-org/mlr/wiki/mlr-Coding-Guidelines).

For some common tasks like integrating another learner or performance measure we have manuals in section "Extend" of the [mlr tutorial](http://mlr-org.github.io/mlr-tutorial/devel/html/). 