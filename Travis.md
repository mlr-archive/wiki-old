# Travis build process

## General

We use the R package [tic](https://github.com/travis-ci/travis-build/pull/1265) to specify actions that should be executed on Travis. Why add another layer on top of Travis?

We build in stages. Stages run sequentially by default. The tutorial stages run in parallel as they do not depend on each other.

### tic

Why add another layer on top of Travis?

* `tic` is ci-agnostic, meaning that the same script will also be valid on other CI systems (e.g. Appveyor for Windows). 
* `tic` makes the deployment of docs easy and transparent. 
* `tic` uses R functions instead of Travis own functions.
* `tic` uses `rcmdcheck::rcmdcheck()` instead of R CMD CHECK. This enhanced version comes with the major  among smaller advantages with the feature of showing the full log of failed tests.

In `.travis.yml` most calls just refer to specfic `tic` calls. These `tic` commands are then specified in `tic.R`. The organization of `tic.R` is similar to Travis (and CIs in general): It uses "stages", i.e. different levels of logical layers that are executed in a specific order (e.g. `before_install` runs before stage `install`).

`tic.R` is subdivided into groups by environment variables referring to specific build stages.

### Stages

* The first two stages build the R package cache. If the cache exists, these stages will finish quickly as they do nothing more than downloading the cache. If the cache needs to be rebuild, stage 1 will install all packages listed in the environment variable `WARMUPPKGS`. Stage 2 then installs all dependencies of `mlr`. To avoid timing out in a stage, `WARMUPPKGS` were selected in that way that the runtime is somewhat equally distributed across both warmup stages. Another word to caching: Cache is only shared between stages with the same environment variable at the time of writing this. However, there is already an open PR so that the cache can be shared across build stages with different env variables: https://github.com/travis-ci/travis-build/pull/1265. This is important as we currently need to build two caches: For the package checking and tutorial creation.
* Stage `check` makes sure that all dependencies are installed and up-to-date and performs the checking of the package including all tests
* Stage 4 builds the HTML version of the tutorial
* Stage 5 builds the PDF version of the tutorial

### Tutorial

* The tutorial is build using the most recent version of `pkgdown` and deployed to the `gh-pages` branch. This way we do not clutter the main repo (an alternative would be to deploy to the `docs/` directory of the `master` branch).
* The PDF version is built using a [wrapper script ](https://github.com/mlr-org/mlr/blob/master/vignettes/tutorial/devel/pdf/_pdf_wrapper.Rmd) with the output format `bookdown::pdf_document2()`. 
* All headers of the tutorial pages start with `h2` as `h1` are needed for the grouping headers of the PDF version. 
* The deployment is done via an ssh key stored in the Travis repo setting. The key was added using `travis::use_travis_deploy()`. Deployment is only performed for non-PR commits to the `master` branch and non-cron builds (cron = automatic daily triggered builds by Travis if no commit happened).

#### Inserting figures

Differs for the HTML and PDF build due to visual appearance of the rendered graphics. You need to specify an HTML and PDF chunk within the tutorial page. Execution is then conditioned on the respective rendering type. Example: 

```{r echo=FALSE, out.width = "400pt", fig.align='center', fig.cap="Nested Resampling Figure", eval = knitr::opts_knit$get("rmarkdown.pandoc.to") == "latex"}
knitr::include_graphics("img/nested_resampling.png")
```

```{r echo=FALSE, out.width = "600px", fig.align='center', fig.cap="Nested Resampling Figure", eval = knitr::opts_knit$get("rmarkdown.pandoc.to") != "latex"}
knitr::include_graphics("https://raw.githubusercontent.com/pat-s/mlr/master/vignettes/tutorial/devel/pdf/img/nested_resampling.png")
```

For some reason we need to use the raw Github URL path for the HTML version as rendering will not work otherwise. Maybe this was fixed meanwhile (I do not know what caused the error in the first place) so you can give it a try using relative paths similar as being used for the PDF version.

TODO: 
* mention `pkgdown.yml` and templates

# Travis debug mode

0. Get your API token from your profile page at: https://travis-ci.org/profile

1. Send a POST request to /job/:job_id/debug replacing the TOKEN and JOB_ID values below:

```bash
#! /usr/bin/env bash  
    curl -s -X POST \
   -H "Content-Type: application/json" \
   -H "Accept: application/json" \
   -H "Travis-API-Version: 3" \
   -H "Authorization: token <TOKEN>" \
   -d '{ "quiet": true }' \
   https://api.travis-ci.org/job/<JOB_ID>/debug 
```

The Job ID is displayed in the build log after expanding "Build system information".

2. Head back to the web UI and in the log of your job. There you should see the following lines to connect to the VM:

Setting up debug tools.
Preparing debug sessions.
Use the following SSH command to access the interactive debugging environment:
ssh ukjiuCEkxBBnRAe32Y8xCH0zj@ny2.tmate.io

3. Connect from your computer using SSH into the interactive session, and once you're done, just type exit and your build will terminate.

Once in the SSH session, these bash functions will come in handy to run the different phases in your build: https://docs.travis-ci.com/user/running-build-in-debug-mode/#Things-to-do-once-you-are-inside-the-debug-VM