1. Travis timeouts and package cache.
    1. We currently have a travis timelimit of 100 minutes (instead of 50) due to Lars asking about this here:
    https://github.com/travis-ci/travis-ci/issues/7173
    1. The mlr travis job installs really many packages, as mlr has really many under SUGGESTS. That can take a very long time on an "empty" machine.
    1. Fortunately, travis supports an R package cache, that we have enabled. So for each new build, only new, updated packages are installed from CRAN.
    1. Assuming that not many new suggested packages have to be updated, a current build takes about 30 min. 
    1. We have a slight problem if the R version on travis is updated, as the package then becomes empty. And we can hit the walltime just because of dependency installation (+ tests). So extra 50 min might help us here already, but if that does not work one can do this:
    Delete the "before_script" and "after_success" section from the travis.yml, and overwrite the 
    "script" section (which would normally check and test the package) with "script: - echo "DONE".       
    Then delete like 50% of the packages from DESCRIPTION. This will partially fill the cache for the 
    next run.





