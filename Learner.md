In MLR, a **learner** is an objects that contains a model type with specialized hyperparameters. A leaner can be created using makeLearner(), trained using train(), and used for prediction using predict().

A learner consists of a list with a rather complicated substructure. Below is an example of the learner "k-Nearest Neighbor":

>root
> |--id = "classif.kknn"
> |--type = "classif"
> |--package = "!kknn"
> |--properties = c("twoclass","multiclass","numerics","factors","prob")
> |--par.set 
> |   |--pars
> |   |  |--k
> |   |  |   |--id = "k"
> |   |  |   |--type = "integer"
> |   |  |   |--len = 1
> |   |  |   |--lower = 1
> |   |  |   |--upper = Inf
> |   |  |   |--values = NULL
> |   |  |   |--cnames = NULL
> |   |  |   |--allow.inf = FALSE
> |   |  |   |--has.default = TRUE
> |   |  |   |--default = 7
> |   |  |   |--trafo = NULL
> |   |  |   |--requires = NULL
> |   |  |   |--tunable = TRUE
> |   |  |   |--special.vals = list()
> |   |  |   |--when = "train"
> |   |  |--distance
> |   |  |   |--id = "distance"
> |   |  |   |--type = "numeric"
> |   |  |   |--len = 1
> |   |  |   |--lower = 0
> |   |  |   |--upper = Inf
> |   |  |   |--values = NULL
> |   |  |   |--cnames = NULL
> |   |  |   |--allow.inf = FALSE
> |   |  |   |--has.default = TRUE
> |   |  |   |--default = 2
> |   |  |   |--trafo = NULL
> |   |  |   |--requires = NULL
> |   |  |   |--tunable = TRUE
> |   |  |   |--special.vals = list()
> |   |  |   |--when = "train"
> |   |  |--kernel
> |   |  |   |--id = "kernel"
> |   |  |   |--type = "discrete"
> |   |  |   |--len = 1
> |   |  |   |--lower = NULL
> |   |  |   |--upper = NULL
> |   |  |   |--values
> |   |  |   |   |--rectangular = "rectangular"
> |   |  |   |   |--triangular = "triangular"
> |   |  |   |   |--epanechnikov = "epanechnikov"
> |   |  |   |   |--biweight = "biweight"
> |   |  |   |   |--triweight = "triweight"
> |   |  |   |   |--cos = "cos"
> |   |  |   |   |--inv = "inv"
> |   |  |   |   |--gaussian = "gaussian"
> |   |  |   |   |--optimal = "optimal"
> |   |  |   |--cnames = NULL
> |   |  |   |--allow.inf = FALSE
> |   |  |   |--has.default = TRUE
> |   |  |   |--default = "optimal"
> |   |  |   |--trafo = NULL
> |   |  |   |--requires = NULL
> |   |  |   |--tunable = TRUE
> |   |  |   |--special.vals = list()
> |   |  |   |--when = "train"
> |   |  |--scale
> |   |  |   |--id = "scale"
> |   |  |   |--type = "logical"
> |   |  |   |--len = 1
> |   |  |   |--lower = NULL
> |   |  |   |--upper = NULL
> |   |  |   |--values
> |   |  |   |   |--TRUE = TRUE
> |   |  |   |   |--FALSE = FALSE
> |   |  |   |--cnames = NULL
> |   |  |   |--allow.inf = FALSE
> |   |  |   |--has.default = TRUE
> |   |  |   |--default = TRUE
> |   |  |   |--trafo = NULL
> |   |  |   |--requires = NULL
> |   |  |   |--tunable = TRUE
> |   |  |   |--special.vals = list()
> |   |  |   |--when = "train"
> |   |--forbidden = NULL
> |--par.vals
> |--predict.type
> |--name
> |--short.name
> |--note
> |--config
> |--fix.factors.prediction
