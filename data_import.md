data_import
================
Ravi Brenner
2024-09-17

This document will show how to import data into R following along with
in class work

## Import FAS litters CSV

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

## Import FAS pups dataset

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

missing data

``` r
litters_df <- 
  read_csv(
    file = "data/FAS_litters.csv",
    skip = 0
  )
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
litters_df
```

    ## # A tibble: 49 × 8
    ##    Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##    <chr> <chr>           <chr>        <chr>                 <dbl>
    ##  1 Con7  #85             19.7         34.7                     20
    ##  2 Con7  #1/2/95/2       27           42                       19
    ##  3 Con7  #5/5/3/83/3-3   26           41.4                     19
    ##  4 Con7  #5/4/2/95/2     28.5         44.1                     19
    ##  5 Con7  #4/2/95/3-3     <NA>         <NA>                     20
    ##  6 Con7  #2/2/95/3-2     <NA>         <NA>                     20
    ##  7 Con7  #1/5/3/83/3-3/2 <NA>         <NA>                     20
    ##  8 Con8  #3/83/3-3       <NA>         <NA>                     20
    ##  9 Con8  #2/95/3         <NA>         <NA>                     20
    ## 10 Con8  #3/5/2/2/95     28.5         <NA>                     20
    ## # ℹ 39 more rows
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

can see gd0_weight and gd18_weight is character which isn’t what we want
inspecting the data, we see a mix of blanks, NAs, and . to indicate
missing values

can fix this in read_csv

``` r
litters_df <- 
  read_csv(
    file = "data/FAS_litters.csv",
    na = c("","NA",".")
  )
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df <- clean_names(litters_df)
```

A nice function to maybe add to my cleaning workflow

``` r
skimr::skim(litters_df)
```

|                                                  |            |
|:-------------------------------------------------|:-----------|
| Name                                             | litters_df |
| Number of rows                                   | 49         |
| Number of columns                                | 8          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |            |
| Column type frequency:                           |            |
| character                                        | 2          |
| numeric                                          | 6          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |            |
| Group variables                                  | None       |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| group         |         0 |             1 |   4 |   4 |     0 |        6 |          0 |
| litter_number |         0 |             1 |   3 |  15 |     0 |       49 |          0 |

**Variable type: numeric**

| skim_variable   | n_missing | complete_rate |  mean |   sd |   p0 |   p25 |   p50 |   p75 | p100 | hist  |
|:----------------|----------:|--------------:|------:|-----:|-----:|------:|------:|------:|-----:|:------|
| gd0_weight      |        15 |          0.69 | 24.38 | 3.28 | 17.0 | 22.30 | 24.10 | 26.67 | 33.4 | ▃▇▇▆▁ |
| gd18_weight     |        17 |          0.65 | 41.52 | 4.05 | 33.4 | 38.88 | 42.25 | 43.80 | 52.7 | ▃▃▇▂▁ |
| gd_of_birth     |         0 |          1.00 | 19.65 | 0.48 | 19.0 | 19.00 | 20.00 | 20.00 | 20.0 | ▅▁▁▁▇ |
| pups_born_alive |         0 |          1.00 |  7.35 | 1.76 |  3.0 |  6.00 |  8.00 |  8.00 | 11.0 | ▁▃▂▇▁ |
| pups_dead_birth |         0 |          1.00 |  0.33 | 0.75 |  0.0 |  0.00 |  0.00 |  0.00 |  4.0 | ▇▂▁▁▁ |
| pups_survive    |         0 |          1.00 |  6.41 | 2.05 |  1.0 |  5.00 |  7.00 |  8.00 |  9.0 | ▁▃▂▇▇ |

what if we code `group` as a factor variable?

``` r
litters_df <- 
  read_csv(
    file = "data/FAS_litters.csv",
    na = c("","NA","."),
    col_types = cols(Group = col_factor())
  )

litters_df <- clean_names(litters_df)
```

## Importing from excel

``` r
mlb_df <- read_excel("data/mlb11.xlsx",
                     sheet = "mlb11")
```

## Importing from SAS

``` r
pulse_df <- read_sas("data/public_pulse_data.sas7bdat")
```

## Never use read.csv()

``` r
litters_df <- read.csv("data/FAS_litters.csv")

litters_df$L
```

    ##  [1] "#85"             "#1/2/95/2"       "#5/5/3/83/3-3"   "#5/4/2/95/2"    
    ##  [5] "#4/2/95/3-3"     "#2/2/95/3-2"     "#1/5/3/83/3-3/2" "#3/83/3-3"      
    ##  [9] "#2/95/3"         "#3/5/2/2/95"     "#5/4/3/83/3"     "#1/6/2/2/95-2"  
    ## [13] "#3/5/3/83/3-3-2" "#2/2/95/2"       "#3/6/2/2/95-3"   "#59"            
    ## [17] "#103"            "#1/82/3-2"       "#3/83/3-2"       "#2/95/2-2"      
    ## [21] "#3/82/3-2"       "#4/2/95/2"       "#5/3/83/5-2"     "#8/110/3-2"     
    ## [25] "#106"            "#94/2"           "#62"             "#84/2"          
    ## [29] "#107"            "#85/2"           "#98"             "#102"           
    ## [33] "#101"            "#111"            "#112"            "#97"            
    ## [37] "#5/93"           "#5/93/2"         "#7/82-3-2"       "#7/110/3-2"     
    ## [41] "#2/95/2"         "#82/4"           "#53"             "#79"            
    ## [45] "#100"            "#4/84"           "#108"            "#99"            
    ## [49] "#110"

This prints too much, and allows you to use partial column names

read_csv doesn’t have these issues (and tibbles are more memory
efficient)

``` r
litters_df <- read_csv("data/FAS_litters.csv")
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
litters_df$L
```

    ## Warning: Unknown or uninitialised column: `L`.

    ## NULL

Never do this:

``` r
litters_df$`Litter Number`
```

    ##  [1] "#85"             "#1/2/95/2"       "#5/5/3/83/3-3"   "#5/4/2/95/2"    
    ##  [5] "#4/2/95/3-3"     "#2/2/95/3-2"     "#1/5/3/83/3-3/2" "#3/83/3-3"      
    ##  [9] "#2/95/3"         "#3/5/2/2/95"     "#5/4/3/83/3"     "#1/6/2/2/95-2"  
    ## [13] "#3/5/3/83/3-3-2" "#2/2/95/2"       "#3/6/2/2/95-3"   "#59"            
    ## [17] "#103"            "#1/82/3-2"       "#3/83/3-2"       "#2/95/2-2"      
    ## [21] "#3/82/3-2"       "#4/2/95/2"       "#5/3/83/5-2"     "#8/110/3-2"     
    ## [25] "#106"            "#94/2"           "#62"             "#84/2"          
    ## [29] "#107"            "#85/2"           "#98"             "#102"           
    ## [33] "#101"            "#111"            "#112"            "#97"            
    ## [37] "#5/93"           "#5/93/2"         "#7/82-3-2"       "#7/110/3-2"     
    ## [41] "#2/95/2"         "#82/4"           "#53"             "#79"            
    ## [45] "#100"            "#4/84"           "#108"            "#99"            
    ## [49] "#110"

Because we really don’t need to/shouldn’t be pulling columns out of our
dataframe
