Create Data - CSB
================
Christopher Prener, Ph.D.
(February 21, 2019)

## Introduction

This notebook creates the Citizens’ Service Bureau Data for the Spring
2019 final projects.

## Dependencies

This notebook requires:

``` r
# tidystl packages
library(stlcsb)

# tidyverse packages
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(readr)

# other packages
library(here)
```

    ## here() starts at /Users/chris/Desktop/csb-data-sp19

## Download Data

This notebook requires data that can be automatically downloaded from
the City of St. Louis via the `stlcsb` package’s `csb_get_data()`
function:

``` r
csb <- csb_get_data(years = 2013:2018)
```

## Subset

There are some variables that we’ll get rid of before exporting the
data, and we’ll get rid of cancelled calls as well:

``` r
csb %>%
  csb_canceled(var = datecancelled) %>%
  select(-probaddtype, -callertype, -neighborhood, -ward, -submitto, -dateinvtdone, -prjcompletedate) -> csb
```

## Write Data

Finally, we’ll write the data to `.csv`:

``` r
write_csv(csb, here("data", "csb.csv"))
```
