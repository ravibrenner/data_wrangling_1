data_import
================
Ravi Brenner
2024-09-17

This document will show how to import data into R

## import FAS litters CSV

``` r
litters_df <- read.csv("./data/FAS_litters.csv") 
```

Look at the dataset briefly

``` r
head(litters_df)
```

    ##   Group Litter.Number GD0.weight GD18.weight GD.of.Birth Pups.born.alive
    ## 1  Con7           #85       19.7        34.7          20               3
    ## 2  Con7     #1/2/95/2         27          42          19               8
    ## 3  Con7 #5/5/3/83/3-3         26        41.4          19               6
    ## 4  Con7   #5/4/2/95/2       28.5        44.1          19               5
    ## 5  Con7   #4/2/95/3-3       <NA>        <NA>          20               6
    ## 6  Con7   #2/2/95/3-2       <NA>                      20               6
    ##   Pups.dead...birth Pups.survive
    ## 1                 4            3
    ## 2                 0            7
    ## 3                 0            5
    ## 4                 1            4
    ## 5                 0            6
    ## 6                 0            4

``` r
tail(litters_df)
```

    ##    Group Litter.Number GD0.weight GD18.weight GD.of.Birth Pups.born.alive
    ## 44  Low8           #79       25.4        43.8          19               8
    ## 45  Low8          #100         20        39.2          20               8
    ## 46  Low8         #4/84       21.8        35.2          20               4
    ## 47  Low8          #108       25.6        47.5          20               8
    ## 48  Low8           #99       23.5          39          20               6
    ## 49  Low8          #110       25.5        42.7          20               7
    ##    Pups.dead...birth Pups.survive
    ## 44                 0            7
    ## 45                 0            7
    ## 46                 0            4
    ## 47                 0            7
    ## 48                 0            5
    ## 49                 0            6

``` r
view(litters_df)
```
