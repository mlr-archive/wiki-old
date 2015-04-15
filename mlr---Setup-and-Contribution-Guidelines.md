mlr - Setup & Contribution Guidelines
=========

To encourage a more structured and organized contribution workflow for <b>mlr</b>, every contributor should try to adhere to the guidelines listed in this wiki. We have also provided basic guidelines (particulary for new Github users) to setup mlr locally so you can immediately start to play around the <b>mlr</b> codebase.

## Version control setup

We assume that git is already installed on your local machine, if not follow [these guidelines](https://help.github.com/articles/set-up-git/). 

Use `git clone` to clone this repo to your local machine:
```
git clone https://github.com/berndbischl/mlr.git
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
git remote add upstream https://github.com/berndbischl/mlr.git
```

or if you have ssh set up you can use that url instead:
```
git remote add upstream git://github.com/berndbischl/mlr.git
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

Once you're happy with your code, please open a [pull request for the main repository](https://github.com/berndbischl/mlr/pulls). This will automatically run [Travis CI](https://travis-ci.org/berndbischl/mlr) on your changes to see if it still builds and all the tests pass. The developer team will get notified automatically of your pull request.

For more information on how to implement code for mlr, please see the [coding guidelines](https://github.com/berndbischl/mlr/wiki/mlr-Coding-Guidelines).