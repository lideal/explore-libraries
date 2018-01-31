01\_explore-libraries\_base.R
================
lideal
Wed Jan 31 14:07:49 2018

Which libraries does R search for packages?

``` r
.libPaths()
```

    ## [1] "C:/Users/lideal/Documents/R/win-library/3.4"
    ## [2] "C:/Program Files/R/R-3.4.3/library"

Installed packages

``` r
## use installed.packages() to get all installed packages
pkg <- as.data.frame(installed.packages())

## how many packages?
nrow(pkg)
```

    ## [1] 89

Exploring the packages

``` r
summary(pkg)
```

    ##        Package                                          LibPath  
    ##  assertthat: 1   C:/Program Files/R/R-3.4.3/library         :30  
    ##  backports : 1   C:/Users/lideal/Documents/R/win-library/3.4:59  
    ##  base      : 1                                                   
    ##  base64enc : 1                                                   
    ##  BH        : 1                                                   
    ##  bindr     : 1                                                   
    ##  (Other)   :83                                                   
    ##     Version          Priority          Depends  
    ##  3.4.3  :15   base       :14   R (>= 3.0.0): 7  
    ##  1.2.0  : 4   recommended:15   R (>= 3.0.2): 5  
    ##  0.1    : 2   NA's       :60   R (>= 3.0.1): 4  
    ##  1.0.0  : 2                    R (>= 3.1)  : 4  
    ##  1.1.0  : 2                    R (>= 3.1.0): 4  
    ##  1.5    : 2                    (Other)     :28  
    ##  (Other):62                    NA's        :37  
    ##                                                                                                                                              Imports  
    ##  utils                                                                                                                                           : 4  
    ##  methods                                                                                                                                         : 3  
    ##  tools                                                                                                                                           : 2  
    ##  assertthat, bindrcpp (>= 0.2), glue (>= 1.1.1), magrittr,\nmethods, pkgconfig, rlang (>= 0.1.2), R6, Rcpp (>= 0.12.7),\ntibble (>= 1.3.1), utils: 1  
    ##  assertthat, crayon, methods                                                                                                                     : 1  
    ##  (Other)                                                                                                                                         :44  
    ##  NA's                                                                                                                                            :34  
    ##                                                LinkingTo 
    ##  Rcpp                                               : 1  
    ##  Rcpp (>= 0.12.0), BH (>= 1.58.0-1), bindrcpp, plogr: 1  
    ##  Rcpp, plogr                                        : 1  
    ##  NA's                                               :86  
    ##                                                          
    ##                                                          
    ##                                                          
    ##                                                                                                                                                                      Suggests 
    ##  testthat                                                                                                                                                                : 6  
    ##  MASS                                                                                                                                                                    : 4  
    ##  methods                                                                                                                                                                 : 2  
    ##  bit64, covr, dbplyr, dtplyr, DBI, ggplot2, hms, knitr, Lahman\n(>= 3.0-1), mgcv, microbenchmark, nycflights13, rmarkdown,\nRMySQL, RPostgreSQL, RSQLite, testthat, withr: 1  
    ##  coda, chron, DAAG, fts, ggplot2, mondate, scales,\nstrucchange, timeDate, timeSeries, tis, tseries, xts                                                                 : 1  
    ##  (Other)                                                                                                                                                                 :57  
    ##  NA's                                                                                                                                                                    :18  
    ##                                   Enhances                License  
    ##  chron                                : 1   MIT + file LICENSE:25  
    ##  data.table, dplyr, htmlwidgets       : 1   Part of R 3.4.3   :15  
    ##  knitr                                : 1   GPL-3             :14  
    ##  MatrixModels, graph, SparseM, sfsmisc: 1   GPL (>= 2)        :10  
    ##  png                                  : 1   GPL-2 | GPL-3     : 7  
    ##  snow, nws, Rmpi                      : 1   GPL               : 4  
    ##  NA's                                 :83   (Other)           :14  
    ##  License_is_FOSS License_restricts_use OS_type    MD5sum  
    ##  yes : 1         NA's:89               NA's:89   NA's:89  
    ##  NA's:88                                                  
    ##                                                           
    ##                                                           
    ##                                                           
    ##                                                           
    ##                                                           
    ##  NeedsCompilation   Built   
    ##  no  :33          3.4.1: 5  
    ##  yes :50          3.4.2: 1  
    ##  NA's: 6          3.4.3:83  
    ##                             
    ##                             
    ##                             
    ## 

``` r
## count some things! inspiration
##   * tabulate by LibPath, Priority, or both
##   * what proportion need compilation?
##   * how break down re: version of R they were built on
table(pkg$Priority)
```

    ## 
    ##        base recommended 
    ##          14          15

``` r
table(pkg$LibPath)
```

    ## 
    ##          C:/Program Files/R/R-3.4.3/library 
    ##                                          30 
    ## C:/Users/lideal/Documents/R/win-library/3.4 
    ##                                          59

``` r
table(pkg$NeedsCompilation)
```

    ## 
    ##  no yes 
    ##  33  50

``` r
table(pkg$Built)
```

    ## 
    ## 3.4.1 3.4.2 3.4.3 
    ##     5     1    83

Reflections

``` r
## reflect on ^^ and make a few notes to yourself; inspiration
##   * does the number of base + recommended packages make sense to you?
##   * how does the result of .libPaths() relate to the result of .Library?

table(pkg$Priority)
```

    ## 
    ##        base recommended 
    ##          14          15

``` r
pkg[which(pkg$Priority == 'base'), ]
```

    ##             Package                            LibPath Version Priority
    ## base           base C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## compiler   compiler C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## datasets   datasets C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## graphics   graphics C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## grDevices grDevices C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## grid           grid C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## methods     methods C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## parallel   parallel C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## splines     splines C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## stats         stats C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## stats4       stats4 C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## tcltk         tcltk C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## tools         tools C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ## utils         utils C:/Program Files/R/R-3.4.3/library   3.4.3     base
    ##           Depends                    Imports LinkingTo
    ## base         <NA>                       <NA>      <NA>
    ## compiler     <NA>                       <NA>      <NA>
    ## datasets     <NA>                       <NA>      <NA>
    ## graphics     <NA>                  grDevices      <NA>
    ## grDevices    <NA>                       <NA>      <NA>
    ## grid         <NA>           grDevices, utils      <NA>
    ## methods      <NA>               utils, stats      <NA>
    ## parallel     <NA>            tools, compiler      <NA>
    ## splines      <NA>            graphics, stats      <NA>
    ## stats        <NA> utils, grDevices, graphics      <NA>
    ## stats4       <NA>   graphics, methods, stats      <NA>
    ## tcltk        <NA>                      utils      <NA>
    ## tools        <NA>                       <NA>      <NA>
    ## utils        <NA>                       <NA>      <NA>
    ##                                           Suggests        Enhances
    ## base                                       methods            <NA>
    ## compiler                                      <NA>            <NA>
    ## datasets                                      <NA>            <NA>
    ## graphics                                      <NA>            <NA>
    ## grDevices                               KernSmooth            <NA>
    ## grid                                       lattice            <NA>
    ## methods                                  codetools            <NA>
    ## parallel                                   methods snow, nws, Rmpi
    ## splines                            Matrix, methods            <NA>
    ## stats     MASS, Matrix, SuppDists, methods, stats4            <NA>
    ## stats4                                        <NA>            <NA>
    ## tcltk                                         <NA>            <NA>
    ## tools               codetools, methods, xml2, curl            <NA>
    ## utils                                 methods, XML            <NA>
    ##                   License License_is_FOSS License_restricts_use OS_type
    ## base      Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## compiler  Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## datasets  Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## graphics  Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## grDevices Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## grid      Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## methods   Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## parallel  Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## splines   Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## stats     Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## stats4    Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## tcltk     Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## tools     Part of R 3.4.3            <NA>                  <NA>    <NA>
    ## utils     Part of R 3.4.3            <NA>                  <NA>    <NA>
    ##           MD5sum NeedsCompilation Built
    ## base        <NA>             <NA> 3.4.3
    ## compiler    <NA>             <NA> 3.4.3
    ## datasets    <NA>             <NA> 3.4.3
    ## graphics    <NA>              yes 3.4.3
    ## grDevices   <NA>              yes 3.4.3
    ## grid        <NA>              yes 3.4.3
    ## methods     <NA>              yes 3.4.3
    ## parallel    <NA>              yes 3.4.3
    ## splines     <NA>              yes 3.4.3
    ## stats       <NA>              yes 3.4.3
    ## stats4      <NA>             <NA> 3.4.3
    ## tcltk       <NA>              yes 3.4.3
    ## tools       <NA>              yes 3.4.3
    ## utils       <NA>              yes 3.4.3

``` r
pkg[which(pkg$Priority == 'recommended'), ]
```

    ##               Package                            LibPath Version
    ## boot             boot C:/Program Files/R/R-3.4.3/library  1.3-20
    ## class           class C:/Program Files/R/R-3.4.3/library  7.3-14
    ## cluster       cluster C:/Program Files/R/R-3.4.3/library   2.0.6
    ## codetools   codetools C:/Program Files/R/R-3.4.3/library  0.2-15
    ## foreign       foreign C:/Program Files/R/R-3.4.3/library  0.8-69
    ## KernSmooth KernSmooth C:/Program Files/R/R-3.4.3/library 2.23-15
    ## lattice       lattice C:/Program Files/R/R-3.4.3/library 0.20-35
    ## MASS             MASS C:/Program Files/R/R-3.4.3/library  7.3-47
    ## Matrix         Matrix C:/Program Files/R/R-3.4.3/library  1.2-12
    ## mgcv             mgcv C:/Program Files/R/R-3.4.3/library  1.8-22
    ## nlme             nlme C:/Program Files/R/R-3.4.3/library 3.1-131
    ## nnet             nnet C:/Program Files/R/R-3.4.3/library  7.3-12
    ## rpart           rpart C:/Program Files/R/R-3.4.3/library  4.1-11
    ## spatial       spatial C:/Program Files/R/R-3.4.3/library  7.3-11
    ## survival     survival C:/Program Files/R/R-3.4.3/library  2.41-3
    ##               Priority                                         Depends
    ## boot       recommended                   R (>= 3.0.0), graphics, stats
    ## class      recommended                      R (>= 3.0.0), stats, utils
    ## cluster    recommended                                    R (>= 3.0.1)
    ## codetools  recommended                                      R (>= 2.1)
    ## foreign    recommended                                    R (>= 3.0.0)
    ## KernSmooth recommended                             R (>= 2.5.0), stats
    ## lattice    recommended                                    R (>= 3.0.0)
    ## MASS       recommended R (>= 3.1.0), grDevices, graphics, stats, utils
    ## Matrix     recommended                                    R (>= 3.0.1)
    ## mgcv       recommended                 R (>= 2.14.0), nlme (>= 3.1-64)
    ## nlme       recommended                                    R (>= 3.0.2)
    ## nnet       recommended                     R (>= 2.14.0), stats, utils
    ## rpart      recommended       R (>= 2.15.0), graphics, stats, grDevices
    ## spatial    recommended            R (>= 3.0.0), graphics, stats, utils
    ## survival   recommended                                   R (>= 2.13.0)
    ##                                                     Imports LinkingTo
    ## boot                                                   <NA>      <NA>
    ## class                                                  MASS      <NA>
    ## cluster                   graphics, grDevices, stats, utils      <NA>
    ## codetools                                              <NA>      <NA>
    ## foreign                               methods, utils, stats      <NA>
    ## KernSmooth                                             <NA>      <NA>
    ## lattice             grid, grDevices, graphics, stats, utils      <NA>
    ## MASS                                                methods      <NA>
    ## Matrix       methods, graphics, grid, stats, utils, lattice      <NA>
    ## mgcv                       methods, stats, graphics, Matrix      <NA>
    ## nlme                        graphics, stats, utils, lattice      <NA>
    ## nnet                                                   <NA>      <NA>
    ## rpart                                                  <NA>      <NA>
    ## spatial                                                <NA>      <NA>
    ## survival   graphics, Matrix, methods, splines, stats, utils      <NA>
    ##                                     Suggests
    ## boot                          MASS, survival
    ## class                                   <NA>
    ## cluster                                 MASS
    ## codetools                               <NA>
    ## foreign                                 <NA>
    ## KernSmooth                              MASS
    ## lattice       KernSmooth, MASS, latticeExtra
    ## MASS           lattice, nlme, nnet, survival
    ## Matrix                            expm, MASS
    ## mgcv       splines, parallel, survival, MASS
    ## nlme                             Hmisc, MASS
    ## nnet                                    MASS
    ## rpart                               survival
    ## spatial                                 MASS
    ## survival                                <NA>
    ##                                         Enhances                   License
    ## boot                                        <NA>                 Unlimited
    ## class                                       <NA>             GPL-2 | GPL-3
    ## cluster                                     <NA>                GPL (>= 2)
    ## codetools                                   <NA>                       GPL
    ## foreign                                     <NA>                GPL (>= 2)
    ## KernSmooth                                  <NA>                 Unlimited
    ## lattice                                    chron                GPL (>= 2)
    ## MASS                                        <NA>             GPL-2 | GPL-3
    ## Matrix     MatrixModels, graph, SparseM, sfsmisc GPL (>= 2) | file LICENCE
    ## mgcv                                        <NA>                GPL (>= 2)
    ## nlme                                        <NA> GPL (>= 2) | file LICENCE
    ## nnet                                        <NA>             GPL-2 | GPL-3
    ## rpart                                       <NA>             GPL-2 | GPL-3
    ## spatial                                     <NA>             GPL-2 | GPL-3
    ## survival                                    <NA>               LGPL (>= 2)
    ##            License_is_FOSS License_restricts_use OS_type MD5sum
    ## boot                  <NA>                  <NA>    <NA>   <NA>
    ## class                 <NA>                  <NA>    <NA>   <NA>
    ## cluster               <NA>                  <NA>    <NA>   <NA>
    ## codetools             <NA>                  <NA>    <NA>   <NA>
    ## foreign               <NA>                  <NA>    <NA>   <NA>
    ## KernSmooth            <NA>                  <NA>    <NA>   <NA>
    ## lattice               <NA>                  <NA>    <NA>   <NA>
    ## MASS                  <NA>                  <NA>    <NA>   <NA>
    ## Matrix                <NA>                  <NA>    <NA>   <NA>
    ## mgcv                  <NA>                  <NA>    <NA>   <NA>
    ## nlme                  <NA>                  <NA>    <NA>   <NA>
    ## nnet                  <NA>                  <NA>    <NA>   <NA>
    ## rpart                 <NA>                  <NA>    <NA>   <NA>
    ## spatial               <NA>                  <NA>    <NA>   <NA>
    ## survival              <NA>                  <NA>    <NA>   <NA>
    ##            NeedsCompilation Built
    ## boot                     no 3.4.3
    ## class                   yes 3.4.3
    ## cluster                 yes 3.4.3
    ## codetools                no 3.4.3
    ## foreign                 yes 3.4.3
    ## KernSmooth              yes 3.4.3
    ## lattice                 yes 3.4.3
    ## MASS                    yes 3.4.3
    ## Matrix                  yes 3.4.3
    ## mgcv                    yes 3.4.3
    ## nlme                    yes 3.4.3
    ## nnet                    yes 3.4.3
    ## rpart                   yes 3.4.3
    ## spatial                 yes 3.4.3
    ## survival                yes 3.4.3

``` r
.libPaths() # gives package source available to R version of current session
```

    ## [1] "C:/Users/lideal/Documents/R/win-library/3.4"
    ## [2] "C:/Program Files/R/R-3.4.3/library"

``` r
.Library # gives package source for all R versions installed on a machine 
```

    ## [1] "C:/PROGRA~1/R/R-34~1.3/library"

Going further

``` r
## if you have time to do more ...

## is every package in .Library either base or recommended?
## study package naming style (all lower case, contains '.', etc
## use `fields` argument to installed.packages() to get more info and use it!
dir(.Library) %in% pkg$Package[which(pkg$Priority %in% c("base", "recommended"))]
```

    ##  [1]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
    ## [12]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
    ## [23]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
