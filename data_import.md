data_import
================
Ravi Brenner
2024-09-17

This document will show how to import data into R

## import FAS litters CSV

``` r
litters_df <- read_csv("./data/FAS_litters.csv") 
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df <- clean_names(litters_df) #from janitor package
```

Look at the dataset briefly

``` r
head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Con7  #85           19.7       34.7                 20               3
    ## 2 Con7  #1/2/95/2     27         42                   19               8
    ## 3 Con7  #5/5/3/83/3-3 26         41.4                 19               6
    ## 4 Con7  #5/4/2/95/2   28.5       44.1                 19               5
    ## 5 Con7  #4/2/95/3-3   <NA>       <NA>                 20               6
    ## 6 Con7  #2/2/95/3-2   <NA>       <NA>                 20               6
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
tail(litters_df)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Low8  #79           25.4       43.8                 19               8
    ## 2 Low8  #100          20         39.2                 20               8
    ## 3 Low8  #4/84         21.8       35.2                 20               4
    ## 4 Low8  #108          25.6       47.5                 20               8
    ## 5 Low8  #99           23.5       39                   20               6
    ## 6 Low8  #110          25.5       42.7                 20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
view(litters_df)
```

## import FAS pups dataset

``` r
pups_df <- read_csv("./data/FAS_pups.csv")

pups_df <- clean_names(pups_df)
```

look at the data

``` r
head(pups_df)
```

    ## # A tibble: 6 × 6
    ##   litter_number   sex pd_ears pd_eyes pd_pivot pd_walk
    ##   <chr>         <dbl> <chr>     <dbl>    <dbl>   <dbl>
    ## 1 #85               1 4            13        7      11
    ## 2 #85               1 4            13        7      12
    ## 3 #1/2/95/2         1 5            13        7       9
    ## 4 #1/2/95/2         1 5            13        8      10
    ## 5 #5/5/3/83/3-3     1 5            13        8      10
    ## 6 #5/5/3/83/3-3     1 5            14        6       9

## look at read_csv options

col_names and skipping rows

``` r
litters_df <- 
  read_csv(
    file = "data/FAS_litters.csv",
    skip = 2
  )
```
