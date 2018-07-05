# Tags
For every issue assign one tag of each category:
* **priority**: 
  * [Low](https://github.com/mlr-org/mlr/labels/prio-low): unimportant stuff like small enhancements 
  * [Medium](https://github.com/mlr-org/mlr/labels/prio-medium): everything that is not low, high or blocking
  * [High](https://github.com/mlr-org/mlr/labels/prio-high): Mainly bugs
  * [blocking](https://github.com/mlr-org/mlr/labels/prio-blocking): Thing like master is broken, basic functionality of mlr is wrong, blocks other high prio PRs.
* **effort**: 
  * [simplefix](https://github.com/mlr-org/mlr/labels/effort-simplefix): Things you can do in a coffee break.
  * [hardfix](https://github.com/mlr-org/mlr/labels/effort-hardfix): You probably need more than a day and a coworker.
  * no tag
* **Type**: 
  * [question](https://github.com/mlr-org/mlr/labels/type-question): Questions that can be answered without touching the code.
  * [enhancement](https://github.com/mlr-org/mlr/labels/type-enhancement): Requests or Suggestions of new functionality.
  * [bug](https://github.com/mlr-org/mlr/labels/type-bug): Functionality broken or not working like advertised.
  * [doc](https://github.com/mlr-org/mlr/labels/type-documentation): Request for a better documentation. Function code does not have to be touched.

Each PR should be tagged with one of the following tags:
* **PR state**: 
  * [work in progress](https://github.com/mlr-org/mlr/labels/work%20in%20progress%20-%20not%20done): The assigned person is working on it. If no person is assigned this PR is looking for an asignee.
  * [ready for merge](https://github.com/mlr-org/mlr/labels/ready%20for%20merge%20%28%3F%29): The PR has been reviewed by one person, who thinks that this is ready to be merged.
  * [please review](https://github.com/mlr-org/mlr/labels/please%20review): The OP has finished work on PR and wants a review or help from a random project member. 
* **priority**:
  * [Low](https://github.com/mlr-org/mlr/pulls?q=is%3Aopen+is%3Apr+label%3Aprio-low)
  * [Medium](https://github.com/mlr-org/mlr/pulls?q=is%3Aopen+is%3Apr+label%3Aprio-medium)
  * [High](https://github.com/mlr-org/mlr/pulls?q=is%3Aopen+is%3Apr+label%3Aprio-high)
  * [blocking](https://github.com/mlr-org/mlr/pulls?q=is%3Aopen+is%3Apr+label%3Aprio-blocking)

# Projects
Try to always put Issues and PRs into their according Projects.
In those projects the issues and PRs should be ordered according to their priority or order in which they have to be solved.