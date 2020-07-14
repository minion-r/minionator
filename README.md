
<!-- README.md is generated from README.Rmd. Please edit that file -->

# minionator

<!-- badges: start -->

<!-- badges: end -->

The goal of minionator is to …

## Installation

You can install the released version of minionator from
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("minionator")
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(minionator)
library(tidyverse)

l <- discrete_matrix(3, 3, 0:2)

row_latin <- tribble(
  ~constraint,             ~variables,
    "alldiff", l %>% filter(row == 0),
    "alldiff", l %>% filter(row == 1),
    "alldiff", l %>% filter(row == 2)
)

column_latin <- tribble(
  ~constraint,             ~variables,
    "alldiff", l %>% filter(col == 0),
    "alldiff", l %>% filter(col == 1),
    "alldiff", l %>% filter(col == 2)
)

list(
          variables = l,
             search = "PRINT ALL",
  unary_constraints = bind_rows(row_latin, column_latin)
) %>%
  minion_output()
#> MINION 3
#> **VARIABLES**
#> DISCRETE l[3,3] {0..2}
#> **SEARCH**
#> PRINT ALL
#> **CONSTRAINTS**
#> alldiff([l[0,0],l[0,1],l[0,2]])
#> alldiff([l[1,0],l[1,1],l[1,2]])
#> alldiff([l[2,0],l[2,1],l[2,2]])
#> alldiff([l[0,0],l[1,0],l[2,0]])
#> alldiff([l[0,1],l[1,1],l[2,1]])
#> alldiff([l[0,2],l[1,2],l[2,2]])
#> 
#> 
#> **EOF**
```
