Homework 2
================

``` r
library(tidyverse)
```

    ## ── Attaching packages ──────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ─────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readxl)
```

## Problem1

Read Mr Trash Data set,

``` r
trashwheel_df =
  read_xlsx ("./data/Trash_data.xlsx",
           sheet = "Mr. Trash Wheel", 
           range= cell_cols("A:N")) %>%
  janitor:: clean_names() %>%
  drop_na(dumpster) %>%
  mutate(sport_balls = round(sports_balls), 
    sports_balls = as.integer(sports_balls)
  )
trashwheel_df
```

    ## # A tibble: 344 x 15
    ##    dumpster month  year date                weight_tons volume_cubic_ya…
    ##       <dbl> <chr> <dbl> <dttm>                    <dbl>            <dbl>
    ##  1        1 May    2014 2014-05-16 00:00:00        4.31               18
    ##  2        2 May    2014 2014-05-16 00:00:00        2.74               13
    ##  3        3 May    2014 2014-05-16 00:00:00        3.45               15
    ##  4        4 May    2014 2014-05-17 00:00:00        3.1                15
    ##  5        5 May    2014 2014-05-17 00:00:00        4.06               18
    ##  6        6 May    2014 2014-05-20 00:00:00        2.71               13
    ##  7        7 May    2014 2014-05-21 00:00:00        1.91                8
    ##  8        8 May    2014 2014-05-28 00:00:00        3.7                16
    ##  9        9 June   2014 2014-06-05 00:00:00        2.52               14
    ## 10       10 June   2014 2014-06-11 00:00:00        3.76               18
    ## # … with 334 more rows, and 9 more variables: plastic_bottles <dbl>,
    ## #   polystyrene <dbl>, cigarette_butts <dbl>, glass_bottles <dbl>,
    ## #   grocery_bags <dbl>, chip_bags <dbl>, sports_balls <int>,
    ## #   homes_powered <dbl>, sport_balls <dbl>

Read and clean Precipitation data 2017 2018

``` r
precip_2018=
   read_xlsx ("./data/Trash_data.xlsx",
              sheet = "2018 Precipitation", 
              skip = 1
              ) %>%
  janitor::clean_names() %>%
  drop_na(month) %>%
  mutate(year=2018) %>%
  relocate(year)
  precip_2018
```

    ## # A tibble: 12 x 3
    ##     year month total
    ##    <dbl> <dbl> <dbl>
    ##  1  2018     1  0.94
    ##  2  2018     2  4.8 
    ##  3  2018     3  2.69
    ##  4  2018     4  4.69
    ##  5  2018     5  9.27
    ##  6  2018     6  4.77
    ##  7  2018     7 10.2 
    ##  8  2018     8  6.45
    ##  9  2018     9 10.5 
    ## 10  2018    10  2.12
    ## 11  2018    11  7.82
    ## 12  2018    12  6.11

``` r
  precip_2017=
   read_xlsx ("./data/Trash_data.xlsx",
              sheet = "2017 Precipitation",
              skip = 1
              ) %>%
  janitor::clean_names() %>%
  drop_na(month) %>%
  mutate(year=2017) %>%
  relocate(year)
  precip_2017
```

    ## # A tibble: 12 x 3
    ##     year month total
    ##    <dbl> <dbl> <dbl>
    ##  1  2017     1  2.34
    ##  2  2017     2  1.46
    ##  3  2017     3  3.57
    ##  4  2017     4  3.99
    ##  5  2017     5  5.64
    ##  6  2017     6  1.4 
    ##  7  2017     7  7.09
    ##  8  2017     8  4.44
    ##  9  2017     9  1.95
    ## 10  2017    10  0   
    ## 11  2017    11  0.11
    ## 12  2017    12  0.94

Combine datasets on annual precipitation

``` r
precip_df= 
  bind_rows(precip_2018, precip_2017) 

month_df = 
  tibble(
    month=1:12, 
    month_name =month.name
  )
month_df
```

    ## # A tibble: 12 x 2
    ##    month month_name
    ##    <int> <chr>     
    ##  1     1 January   
    ##  2     2 February  
    ##  3     3 March     
    ##  4     4 April     
    ##  5     5 May       
    ##  6     6 June      
    ##  7     7 July      
    ##  8     8 August    
    ##  9     9 September 
    ## 10    10 October   
    ## 11    11 November  
    ## 12    12 December

``` r
precip_df
```

    ## # A tibble: 24 x 3
    ##     year month total
    ##    <dbl> <dbl> <dbl>
    ##  1  2018     1  0.94
    ##  2  2018     2  4.8 
    ##  3  2018     3  2.69
    ##  4  2018     4  4.69
    ##  5  2018     5  9.27
    ##  6  2018     6  4.77
    ##  7  2018     7 10.2 
    ##  8  2018     8  6.45
    ##  9  2018     9 10.5 
    ## 10  2018    10  2.12
    ## # … with 14 more rows

``` r
left_join(precip_df, month_df, by="month")
```

    ## # A tibble: 24 x 4
    ##     year month total month_name
    ##    <dbl> <dbl> <dbl> <chr>     
    ##  1  2018     1  0.94 January   
    ##  2  2018     2  4.8  February  
    ##  3  2018     3  2.69 March     
    ##  4  2018     4  4.69 April     
    ##  5  2018     5  9.27 May       
    ##  6  2018     6  4.77 June      
    ##  7  2018     7 10.2  July      
    ##  8  2018     8  6.45 August    
    ##  9  2018     9 10.5  September 
    ## 10  2018    10  2.12 October   
    ## # … with 14 more rows

The dataset information is from the Mr.Trashwheel collector in
Baltimore, Maryland. As trash enters the inner harbor, the trashwheel
collects that trash, and stores it in a dumpster. the dataset contains
information on year, month, and trash collected, include some specific
kinds of trash. There are a total of 344 rows in our final dataset.
Additional data sheets include month precipitation data.

## Problem 2

``` r
transit_df = 
  read_csv("./data2/NYC_Transit.csv") %>%
  janitor::clean_names() %>%
  select(line,station_name, station_latitude, station_longitude, route1, route2, route3, route4, route5, route6, route7, route8, route9, route10, route11, entry, vending, entrance_type, ada )  %>%
mutate(entry = recode(entry, "YES" ="TRUE", "NO" = "FALSE"))
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_character(),
    ##   `Station Latitude` = col_double(),
    ##   `Station Longitude` = col_double(),
    ##   Route8 = col_double(),
    ##   Route9 = col_double(),
    ##   Route10 = col_double(),
    ##   Route11 = col_double(),
    ##   ADA = col_logical(),
    ##   `Free Crossover` = col_logical(),
    ##   `Entrance Latitude` = col_double(),
    ##   `Entrance Longitude` = col_double()
    ## )

    ## See spec(...) for full column specifications.

``` r
  transit_df
```

    ## # A tibble: 1,868 x 19
    ##    line  station_name station_latitude station_longitu… route1 route2 route3
    ##    <chr> <chr>                   <dbl>            <dbl> <chr>  <chr>  <chr> 
    ##  1 4 Av… 25th St                  40.7            -74.0 R      <NA>   <NA>  
    ##  2 4 Av… 25th St                  40.7            -74.0 R      <NA>   <NA>  
    ##  3 4 Av… 36th St                  40.7            -74.0 N      R      <NA>  
    ##  4 4 Av… 36th St                  40.7            -74.0 N      R      <NA>  
    ##  5 4 Av… 36th St                  40.7            -74.0 N      R      <NA>  
    ##  6 4 Av… 45th St                  40.6            -74.0 R      <NA>   <NA>  
    ##  7 4 Av… 45th St                  40.6            -74.0 R      <NA>   <NA>  
    ##  8 4 Av… 45th St                  40.6            -74.0 R      <NA>   <NA>  
    ##  9 4 Av… 45th St                  40.6            -74.0 R      <NA>   <NA>  
    ## 10 4 Av… 53rd St                  40.6            -74.0 R      <NA>   <NA>  
    ## # … with 1,858 more rows, and 12 more variables: route4 <chr>, route5 <chr>,
    ## #   route6 <chr>, route7 <chr>, route8 <dbl>, route9 <dbl>, route10 <dbl>,
    ## #   route11 <dbl>, entry <chr>, vending <chr>, entrance_type <chr>, ada <lgl>

The dataset contains information from the transit system in NYC. The
variables line, station\_name, station\_latitude, station\_longitude,
route1, route2, route3, route4, route5, route6, route7, route8, route9,
route10, route11, entry, vending, entrance\_type, ada. In order to clean
the data I used the Janitor function to turn the variable names into
snakecase I then selected for our variables of interest in order to
eliminate unwanted clutter variables. The dataset is 1868 rows and 19
columns.

There are 465 stations and 84 are ADA compliant. The proportion of
station entrances / exits without vending allow entrance is 0.4343434
