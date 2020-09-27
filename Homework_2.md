Homework 2
================

``` r
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ──────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readxl)
```

## Problem1

Read Mr Trash Data set,

``` r
trashwheel_df =
  read_xlsx ("./data/Trash_data.xlsx")
```

    ## New names:
    ## * `` -> ...15
    ## * `` -> ...16
    ## * `` -> ...17

``` r
trashwheel_df
```

    ## # A tibble: 406 x 17
    ##    Dumpster Month  Year Date                `Weight (tons)` `Volume (cubic …
    ##       <dbl> <chr> <dbl> <dttm>                        <dbl>            <dbl>
    ##  1        1 May    2014 2014-05-16 00:00:00            4.31               18
    ##  2        2 May    2014 2014-05-16 00:00:00            2.74               13
    ##  3        3 May    2014 2014-05-16 00:00:00            3.45               15
    ##  4        4 May    2014 2014-05-17 00:00:00            3.1                15
    ##  5        5 May    2014 2014-05-17 00:00:00            4.06               18
    ##  6        6 May    2014 2014-05-20 00:00:00            2.71               13
    ##  7        7 May    2014 2014-05-21 00:00:00            1.91                8
    ##  8        8 May    2014 2014-05-28 00:00:00            3.7                16
    ##  9       NA May …    NA NA                            26.0               116
    ## 10        9 June   2014 2014-06-05 00:00:00            2.52               14
    ## # … with 396 more rows, and 11 more variables: `Plastic Bottles` <dbl>,
    ## #   Polystyrene <dbl>, `Cigarette Butts` <dbl>, `Glass Bottles` <dbl>, `Grocery
    ## #   Bags` <dbl>, `Chip Bags` <dbl>, `Sports Balls` <dbl>, `Homes
    ## #   Powered*` <dbl>, ...15 <chr>, ...16 <lgl>, ...17 <lgl>
