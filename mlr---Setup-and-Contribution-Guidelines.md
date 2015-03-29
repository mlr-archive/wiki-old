mlr - Setup & Contribution Guidelines
=========

To encourage a more structured and organized contribution workflow for <b>mlr</b>, every contributor should try to adhere to the guidelines listed in this wiki. We have also provided basic guidelines (particulary for new Github users) to setup mlr locally so you can immediately start to play around the <b>mlr</b> codebase.

## Run Locally
We assume that git is already installed on your local machine, if not follow [these guidelines](https://help.github.com/articles/set-up-git/). 

Use `git clone` to clone this repo to your local machine:
```
git https://github.com/berndbischl/mlr.git
```
<br>
`cd` into cloned repo:
```
cd mlr
```

We suppose you have already got R and RStudio setup on your local machine. If not then you can follow the instructions given [here](http://cran.r-project.org/bin/linux/ubuntu/README.html) and [here](http://www.rstudio.com/products/rstudio/#Desk). 

Once your RStudio is up and running, you can simply open mlr project by clicking on file -> New Project -> Existing Directory (Browse the mlr project).

## Contribution Guidelines

Fork this repository to your account, using the **Fork** button on the top right corner.

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
git remote add upstream git@github.com:/berndbischl/mlr.git
```

<br>
Working branch for **mlr** is the `master` branch. Hence, all the latest code will always be on the *master* branch.
You should always create a new branch for any new piece of work branching from *master* branch:
```
git branch new_branch
```
**NOTE:** You must not mess with `master` branch or bad things will happen.
*master* branch contains the latest stable code, so just leave it be.

Before starting any new piece of work, move to *master* branch:
```
git checkout master
```
<br>
Now you can fetch latest changes from parent repo using:
```
git fetch upstream
```
<br>
`merge` the latest code with *master* branch:
```
git merge upstream/master
```
<br>
`checkout` to your newly created branch:
```
git checkout new_branch
```
<br>
Rebase the code of *new_branch* from the code in *master* branch, run the `rebase` command from your current branch:
```
git rebase master
```
Now all your changes on your current branch will be based on top of the changes in *master* branch.

<b>Note: </b> It's imperative to write meaningful commit messages, mlr developer community is growing every day and other developers should be able to make sense of the work you have done, by your commit changes. Simply writing "made some changes" or something on similar lines is not a good practice. So try to write short and clear commit messages.

Push your changes to your forked repo
```
git push origin new_branch
```
<br>
Now, you can simply send the Pull Request to Parent Repo from your forked Repo on Github.

### Thanks for making mlr even better ;)