Implementing existing plotting functionality with [ggvis](http://ggvis.rstudio.com/) (v 0.4). 

The existing functions for plotting when I started this were
- `plotROCRCurves`
- `plotTuneMultiCritResult`
- `plotThreshVsPerf`
- `plotFilterValues`
- `plotLearningCurve`

All of these had `ggplot2` implementations. I started by creating static `ggvis` implementations of each of these. Some notes on doing so are below.

`ggvis` makes heavy use of non-standard evaluation and pipes (in the vignettes anyway) and is designed (understandably) for interactive use. so that it will pass check it is necessary to add "properties" (the `ggvis` version of `ggplot2`'s aesthetics) manually. This is covered fairly well on the [properties and scales](http://ggvis.rstudio.com/properties-scales.html) section of the docs.

```{r}
library(ggvis)
# standard ggvis syntax
ggvis(iris, ~Sepal.Length, ~Sepal.Width) %>% layer_points()
# package version
plt = ggvis::ggvis(iris, ggvis::prop("x", as.name("Sepal.length")), ggvis::prop("y", as.name("Sepal.Width")))
ggvis::layer_points(plt)
```
The group aesthetic is not in `ggvis`. To group properties (e.g. lines, points) by a factor variable use the `group_by` method. When using this interactively you can pipe to it, but if not you have to reference the method directly (i.e. `ggvis::group_by_.ggvis`). This is not documented anywhere I could find.

Color is now controlled with `stroke` and is pretty well described in the [layers](http://ggvis.rstudio.com/layers.html) section of the docs.

Some simple things, like adding a line defined by one or two parameters, lack convenience functions like `geom_abline`, `geom_vline`, etc. This can be worked around with `layer_lines` fairly easily however.

Generating interactivity is handled via [Shiny](http://shiny.rstudio.com/), which is a dynamic web application framework. For interactivity it is necessary to have a connected R session (RStudio offers a free server with one R process and have paid tiers with more). Locally this just means that an interactive plot starts a local server which then opens in the default browser. If you are using RStudio it will open in the plot window. There are some functions in `ggvis` which generate interactivity, but mostly this is supposed to be generated by making objects that the plot depends on "reactive."

I would estimate that I spent around 5-6 hours reading the `ggvis` docs, looking at the [source](https://github.com/rstudio/ggvis/), and toying around with examples before I started implementing the static functionality. For functions which `ggvis` had a direct mapping to `ggplot2` (they have a [nice table](http://ggvis.rstudio.com/ggplot2.html) on this as well) I spent about an hour on each function. Since then I've spent time moving things around (after we decided to keep the `ggplot2` and `ggvis` versions and to make the computation separate). I am currently still in the process of doing that.

Uncovered in the process is that some functionality in `ggplot2` is not available in `ggvis`. Notably facetting and/or subplotting are missing. It says on the [layers](http://ggvis.rstudio.com/layers.html) page of the docs that this is supported in [Vega](https://trifacta.github.io/vega/) (group_mark) and will be forthcoming in a future release of `ggvis`. At that point I think we/I can go back and add that functionality. It is currently only an issue with `plotLearningCurve`, which can take multiple learners and multiple measures. I have currently worked around the problem by mapping one of those things to color (stroke) and the other to a interactive drop down menu (using a small shiny app). I was thinking that it would be good to have a generic shiny app for `mlr`, but I think it is sufficiently easy and already quite general (essentially no boilerplate code is required) that we should have one for each plotting function for which interactivity is desired. It took me maybe 3-4 hours to go from knowing little/nothing of Shiny to having the above mentioned interactive functionality.

I think that the current plan should be to have a default ggplot version which takes the standard function name (e.g. `plotLearnerPrediction`) and an additional `ggvis` version (e.g. `plotLearnerPrediction_ggvis`). The `ggvis` function will be interactive or static depending on a flag and the users input, and will be different from function to function (e.g. some have tooltips, others drop down menus, etc.). I also plan on expanding some of the plot data generating functions (e.g. to take lists of learners, measures, etc.) so that the interactivity can be more fully taken advantage of. With the eventual addition of subplotting/facetting I think this will be quite nice for exploring learners during research. Eventually we can maybe reverse this naming scheme, so the `ggvis` version is the default and there is an extra `ggplot2` version available.

A few other notes. I have left `plotLearnerPrediction` alone for now, as that will be my next major task (to separate out its functionality and add some new things).

I have, along the way, been using the `ggplot2`/`ggvis` defaults for the sizing of layers, rather than adding lots of arguments to the function to allow maximal user control. I think allowing lots of user control is undesirable for this sort of functionality, which, to my mind, is supposed to be for interactive use during the research process, not the generation of publication quality figures. For that we have exposed (or are in the process of exposing) all of the plot data generation functions, which allows users to create their own graphics. This has included removing some existing arguments which have created new `mlr` specific defaults.

It is possible to embed static `ggvis` plots in `html` documents (dynamic visualizations are somehow converted to static versions with a warning). I have figured out that (seemingly) all of the rendering of .Rmd files with ggvis plots is done using [rmarkdown](https://github.com/rstudio/rmarkdown), specifically rmarkdown::render. This uses knitr first and then calls pandoc which now is packaged with RStudio (this is called by the "knit HTML" button in RStudio). The call to `knitr` is vanilla (no special options). However with `pandoc` it is necessary to include several javascript libraries which are packaged in `ggvis` for the plots to render in html. Specifically, `jquery`, `vega`, `lodash`, `d3`, and a `ggvis.js` file. All are minified and packaged with `ggvis`. Creating a html file which has the paths to these files wrapped in `<script>` tags and using the `--include-in-header` flag with `pandoc` renders the plots. `rmarkdown::render` additionally includes themes (bootstrap) and some other options.

I used [this](https://raw.githubusercontent.com/rstudio/ggvis/master/demo/rmarkdown/html_document.Rmd) as my test page, and named it `test.Rmd`.

This can be rendered first by using `rmarkdown::render("test.Rmd")`, which generates `test.html`.

Alternatively you can first run `knitr`: `knitr::knit("test.Rmd", "test.md")`, create a file `test_include.html` shown below (this is the version automatically created by `rmarkdown::render` internally on my system).

```{html}
<script src="/Users/zmjones/Library/R/3.2/library/rmarkdown/rmd/h/jquery-1.11.0/jquery.min.js"></script>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<link href="/Users/zmjones/Library/R/3.2/library/rmarkdown/rmd/h/bootstrap-3.3.1/css/bootstrap.min.css" rel="stylesheet" />
<script src="/Users/zmjones/Library/R/3.2/library/rmarkdown/rmd/h/bootstrap-3.3.1/js/bootstrap.min.js"></script>
<script src="/Users/zmjones/Library/R/3.2/library/rmarkdown/rmd/h/bootstrap-3.3.1/shim/html5shiv.min.js"></script>
<script src="/Users/zmjones/Library/R/3.2/library/rmarkdown/rmd/h/bootstrap-3.3.1/shim/respond.min.js"></script>
<link href="/Users/zmjones/Library/R/3.2/library/ggvis/www/lib/jquery-ui/css/smoothness/jquery-ui-1.10.4.custom.min.css" rel="stylesheet" />
<script src="/Users/zmjones/Library/R/3.2/library/ggvis/www/lib/jquery-ui/js/jquery-ui-1.10.4.custom.min.js"></script>
<script src="/Users/zmjones/Library/R/3.2/library/ggvis/www/lib/d3/d3.min.js"></script>
<script src="/Users/zmjones/Library/R/3.2/library/ggvis/www/lib/vega/vega.min.js"></script>
<script src="/Users/zmjones/Library/R/3.2/library/ggvis/www/lib/lodash/lodash.min.js"></script>
<script>var lodash = _.noConflict();</script>
<link href="/Users/zmjones/Library/R/3.2/library/ggvis/www/ggvis/css/ggvis.css" rel="stylesheet" />
<script src="/Users/zmjones/Library/R/3.2/library/ggvis/www/ggvis/js/ggvis.js"></script>
```

Rendering to html can be handled by calling `pandoc` from the command line.

`pandoc --include-in-header test_include.html test.md -o test.html`