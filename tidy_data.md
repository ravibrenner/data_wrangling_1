Tidying Data
================
2024-09-24

``` r
library(tidyverse)
library(readxl)
library(haven)
```

This document will show how to tidy data.

## Pivot longer with `pivot_longer`

``` r
pulse_df <-
  read_sas("data/public_pulse_data.sas7bdat") |>
  janitor::clean_names() |>
  pivot_longer(
    cols = bdi_score_bl:bdi_score_12m,
    names_to = "visit",
    values_to = "bdi_score",
    names_prefix = "bdi_score_"
  ) |>
  mutate(visit = replace(visit, visit == "bl", "00m")) |>
  relocate(id, visit)
```

One more example

``` r
litters_df <- read_csv("data/FAS_litters.csv",
                       na = c("NA","","."),
                       show_col_types = FALSE) |>
  janitor::clean_names() |>
  pivot_longer(cols = gd0_weight:gd18_weight,
               names_to = "gd_time",
               values_to = "weight") |>
  mutate(gd_time = case_match(gd_time,
                              "gd0_weight" ~ 0,
                              "gd18_weight" ~ 18))
```

## Pivot wider with `pivot_wider`

Make up some analysis results

``` r
analysis_df <-
  tibble(
    group = c("treatment", "treatment", "control", "control"),
    time = c("pre", "post", "pre", "post"),
    mean = c(4, 10, 4.2, 5)
  )
```

`pivot_wider` for human readability.

``` r
analysis_df |>
  pivot_wider(names_from = "time",
              values_from = "mean") |>
  knitr::kable()
```

| group     | pre | post |
|:----------|----:|-----:|
| treatment | 4.0 |   10 |
| control   | 4.2 |    5 |

## Bind tables

``` r
fellowship_ring <- read_excel("data/LotR_Words.xlsx", 
                              range = "B3:D6") |>
  mutate(movie = "fellowship_ring")

two_towers <- read_excel("data/LotR_Words.xlsx", 
                         range = "F3:H6") |>
  mutate(movie = "two_towers")

return_king <- read_excel("data/LotR_Words.xlsx", 
                          range = "J3:L6") |>
  mutate(movie = "return_king")

lotr_df <- bind_rows(fellowship_ring, two_towers, return_king) |>
  janitor::clean_names() |>
  pivot_longer(col = female:male,
               names_to = "sex",
               values_to = "words") |>
  relocate(movie) |>
  mutate(race = str_to_lower(race))
```

## Relational data

Litters df

``` r
litters_df <-
  read_csv("data/FAS_litters.csv", na = c("", "NA", ".")) |>
  janitor::clean_names() |>
  mutate(wt_gain = gd18_weight - gd0_weight) |>
  separate(group,
           into = c("dose", "day_of_treatment"),
           sep = 3)
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

pups df

``` r
pups_df <-
  read_csv("data/FAS_pups.csv", na = c("", "NA", ".")) |>
  janitor::clean_names() |>
  mutate(sex = case_match(sex,
                          1 ~ "male",
                          2 ~ "female"))
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Join the datasets

``` r
fas_df <-
  left_join(pups_df,litters_df, by = "litter_number") |>
  relocate(litter_number, dose, day_of_treatment)
```
