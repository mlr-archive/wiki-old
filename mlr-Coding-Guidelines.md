We use a git “gatekeeper” workflow model, where every code change to the master branch, whether from the main developers or outside contributors, should be a pull request, which is then checked and possibly refined through reviews. How this works in detail is outlined below. If you have questions, feel free to ask in the tracker, we are happy to help.

- Every change to the code **must** be a pull request. Lars, Michel and Bernd have the license to directly push to the master branch and merge PRs. But it is strongly encouraged that they issue pull requests, too. Nobody should merge his own PR.
- To update a branch, pull in the latest updates from the master into your branch with a **merge**. Do not rebase, especially if multiple people are working on the same branch.
- Use a descriptive title. Add some text explaining what you did and what the purpose is. Include examples of any new output, plots, etc. And please refer to the issue you are dealing with by a link in the text. Including the number in the title is good, but this is not clickable.
- Every major change to **mlr’s core system**, i.e., training, resampling, wrappers, etc, has to be **reviewed by 2 persons**.
  - The pull request can contain multiple commits, they will be squashed when the pull request is merged. Since this is done automatically by GitHub, it's not necessary for you to squash to 1 commit yourself.
- Here is a minimal check list before pull requests can be merged. Do **not** deviate from this without asking / a proper reason!
  - Travis passes. But also **always** check the output for NOTES and WARNINGS from R.
  - Unit tests added/changed as appropriate. **Every** detected bug, major addition or change must result in a **new, good test**. If your test relies on specific learner behavior, use a [mock learner](https://github.com/mlr-org/mlr/blob/master/tests/testthat/helper_mock_learners.R).
  - Did you think carefully about the names (especially exported functions) that you introduced? This is very important and hard to change later.
  - Please use the proper Roxygen tags/templates in the documentation. See [this directory](https://github.com/mlr-org/mlr/tree/master/man-roxygen) for templates we use.
  - Did you document all arguments and return values, including their types? Did you include references to relevant papers?
  - Please include examples on how the new function can be used in the documentation.
  - Did you use the stringi functions for string operations?
  - Did you use the appropriate functions for argument checking (some provided by mlr `check*`, others by the checkmate package).
  - mlr provides many functions to get information from its objects. Please use those instead of `$`.
  - NEWS: Is it an API / behavior change w.r.t. to the prior version? Mention what should be in NEWS in the pull request please, the person who merges the PR will put this in NEWS. Please don't modify NEWS directly as this tends to cause merge conflicts.
  - Code readable, commented and follows [style guide](https://github.com/tudo-r/PackagesInfo/wiki/R-Style-Guide)?
  - Is it an API change? Has the documentation at **all** relevant places been adapted? This includes the tutorial.
  - **The old API cannot be changed so existing client code breaks**. Sometimes such a change is unavoidable and preferable to improve the structure and the exported names of the package. Then use the “deprecate” mechanism explained below.
  - Make sure that no document files (*.rd), NAMESPACE file(s) are changed, as they will be updated automatically.
  - Make sure that only files are changed that are related to the PR. It can happen from time to time that your editor will add/remove whitespaces or indentation automatically.
  - Make sure that no spelling errors are in the documentation. Run a spellchecker (in RStudio you can use F7) 

## General rules

Read those if you are new to the project.
- Use a proper editor for programming. Like vim, emacs, sublime, RStudio.
- Read and follow the [style guide](https://github.com/tudo-r/PackagesInfo/wiki/R-Style-Guide). Yes, really. Bernd hates cleaning up such stuff behind others. If you use RStudio, these settings will help:
  - Whitespace after, e.g., `if` and `for` can be automatically identified in RStudio: Go to \
[Tools -> Global Options... -> Code -> Diagnostics -> activate "Show diagnostics for R" and "Provide R style diagnostics (e.g. whitespace)"](https://support.rstudio.com/hc/en-us/articles/205753617-Code-Diagnostics?version=1.0.136&mode=desktop).
  - For proper indentation go to: Tools -> Global Options... -> Code -> Editing -> deactivate "Vertically align arguments in auto-indent".
  - To automatically remove whitespace go to: Tools -> Global Options... -> Code -> Saving -> activate "Ensure that source files end with newline" and "Strip trailing horizontal whitespace when saving".
- Whatever you implement, you will document in roxygen. Look at other functions to see how this works. Input / Output? What happens in the method? Mention really important details? Like "@family", dislike "@seealso". In summary: Be brief, but precise and helpful to the user!
- Every longer, more complex operation get commented properly in code. See style guide.
- Every function that implements functionality described in the literature should be explained and the relevant literature cited.
  - Explain the high-level concept in the documentation so that reading the paper is not necessary for a basic understanding.
  - Cite the paper using roxygen @references [Author A], [Author B], and [Author C]; [Title: Subtitle], [Journal Volume x] ([Year]), ..., [?Pages].
- We like [Michel's "rt" tool](https://github.com/rdatsci/rt) here. Maybe you like it too?
- Before you push you will run at least once at the end
  - The relevant unit tests. Often this is the group "base" with "rtest --filter=base".
  - "R CMD check" or "rcheck". No errors, warnings, notes!
- Your unit tests and R examples will be the perfect compromise between
  - They test / demo everything relevant.
  - They run really fast. Maybe in much less then a second. Yes, sometimes difficult, but work on it.
- If you find a bug, always do this: Reproduce via test, THEN repair. Then make sure test runs. Reread the code piece again you touched. Can the structure be improved? If this can be done quickly, do it now. For more complex stuff: Open up a clearly understandable issue. Best with a minimal example that reproduces the bug.
- If you do change the API:
  - Deprecate the old code, use [`.Deprecated()`](https://stat.ethz.ch/R-manual/R-devel/library/base/html/Deprecated.html) at the beginning of the deprecated method. This only outputs a warning, it doesn’t automatically call the new function.
  - Carefully explain what you did so we can add that information to NEWS.
- Reference functions in package that are in suggests using `::`, e.g., `package::function`, but do not explicitly reference functions in packages that are imported.
- Please use a spellchecker, especially for documentation. In rstudio you can start a spellcheck with F7.              

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

Then change back to your new branch and merge your changes.
```
git checkout new_branch
git merge master
```
Now all changes from the *master* will be in your current branch.


### Merging the *master* in you branch
This happens quite often and is mostly done wrong. Here is one way to do it correctly:

Firstly, we build the NAMESPACE and Documentation Files automatically on the master branch, which means that if you pull the master branch you have the latest version of the NAMESPACE and all .Rd Files (which are most likely not up to date on your branch, as you shouldn't add/commit any of these).

If you merge the master in your branch all of these files will appear as modified ("green" in git status). You can just commit these as they are identical on the master and will not change the PR. 
BUT(!!!): This is only the case if you don't have any modified files in your branch before(!) you merge the master. Otherwise strange stuff can and will happen.

General workflow:

- git checkout master
- git pull 
- git checkout YOURBRANCH
- git add XXX
- git commit -m "stuff" # commit everything you need from your branch, everthing else should be deleted
- git reset HEAD --hard #This removes/deletes all uncommited files, make sure to add+commit everything you want to keep
- rm XXX # remove all files that are untracked as they might give you mergeconflicts
- git merge master
- (potentially resolve merge conflicts -> use a tool for that -> http://meldmerge.org/)
- git commit -m "resolved mergeconflicts | merged master"
- git push origin YOURBRANCH

If all of that was already clear for you: great :)
Also if you have a slightly different workflow (e.g. use git clean) that works the same way, keep doing that. Above is just how I tend to do it.

## Testing

mlr has a lot of tests for all sorts of functionality. Unfortunately, this makes it quite hard to run as a lot of packages need to be installed for everything to pass. There are several ways to run the tests locally:

- Use `devtools::test` with a filter, for example `devtools::test(filter = "ModelMultiplexer")` to check a particular file and later, when that runs, check whether your code affected other parts of mlr run the test group "base": `devtools::test(filter = "base")`. There are more tests, but the main functionality is covered by the "base" group.
- You can also run tests from the command line, with a fully installed development version of mlr. You can use the [rt tool](https://github.com/rdatsci/rt) for this, for example `rtest --filter=ModelMultiplexer` or `rtest --filter=base`.

To make really sure, we run Travis CI for every commit and pull request. This is your safety net that will check everything for you, so don't worry if you absolutely cannot get something to work on your machine!

## Contributing

Once you're happy with your code, please open a [pull request for the main repository](https://github.com/mlr-org/mlr/pulls). This will automatically run [Travis CI](https://travis-ci.org/mlr-org/mlr) on your changes to see if it still builds and all the tests pass. The developer team will get notified automatically of your pull request.

For some common tasks like integrating another learner or performance measure we have manuals in section "Extend" of the [mlr tutorial](http://mlr-org.github.io/mlr-tutorial/devel/html/). 