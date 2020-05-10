Admissions Analysis
================
Daniel O’Leary
4/17/2020

  - [Setup](#setup)
      - [Load Packages](#load-packages)
      - [Load Data](#load-data)
  - [Analysis](#analysis)
      - [Total number of apps by area](#total-number-of-apps-by-area)
          - [Counts from eth\_summaries](#counts-from-eth_summaries)
          - [Counts from n\_applicants
            file](#counts-from-n_applicants-file)

# Setup

## Load Packages

``` r
if (!require("pacman")) install.packages("pacman")
```

    ## Loading required package: pacman

``` r
pacman::p_load(tidyverse)
```

## Load Data

``` r
eth <- 
  read_csv("C:/Users/Daniel/OneDrive - Leland Stanford Junior University/dc/applicant_analysis/applicant_analysis/results/eth_summaries.csv") 
```

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_character(),
    ##   Affective = col_double(),
    ##   Cognitive = col_double(),
    ##   Developmental = col_double(),
    ##   Neuroscience = col_double(),
    ##   Social = col_double(),
    ##   season = col_character()
    ## )

``` r
gender <- 
  read_csv("C:/Users/Daniel/OneDrive - Leland Stanford Junior University/dc/applicant_analysis/applicant_analysis/results/gender.csv") 
```

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_character(),
    ##   `2017-18` = col_double(),
    ##   `2018-19` = col_double(),
    ##   `2019-20` = col_double()
    ## )

``` r
n_applicants <- 
  read_csv("C:/Users/Daniel/OneDrive - Leland Stanford Junior University/dc/applicant_analysis/applicant_analysis/results/n_applicants.csv") 
```

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_character(),
    ##   `2017-18` = col_double(),
    ##   `2018-19` = col_double(),
    ##   `2019-20` = col_double()
    ## )

``` r
eth <-
  eth %>% 
  mutate(eth = X1) %>% 
  dplyr::select(-X1)

gender <-
  gender %>% 
  mutate(area = X1) %>% 
  dplyr::select(-X1)

n_applicants <-
  n_applicants %>% 
  mutate(area = X1) %>% 
  dplyr::select(-X1)
```

# Analysis

## Total number of apps by area

### Counts from eth\_summaries

``` r
eth %>% 
  gather(area, value, Affective:Social) %>% 
  count(area, season, wt = value) %>% 
  mutate(
    total_apps = n
  ) %>% 
  dplyr::select(-c(n)) %>% 
  arrange(season)
```

    ## # A tibble: 15 x 3
    ##    area          season  total_apps
    ##    <chr>         <chr>        <dbl>
    ##  1 Affective     2017-18        138
    ##  2 Cognitive     2017-18         55
    ##  3 Developmental 2017-18        117
    ##  4 Neuroscience  2017-18         76
    ##  5 Social        2017-18        207
    ##  6 Affective     2018-19        160
    ##  7 Cognitive     2018-19         43
    ##  8 Developmental 2018-19        161
    ##  9 Neuroscience  2018-19         52
    ## 10 Social        2018-19        242
    ## 11 Affective     2019-20        223
    ## 12 Cognitive     2019-20         71
    ## 13 Developmental 2019-20        225
    ## 14 Neuroscience  2019-20        104
    ## 15 Social        2019-20        267

### Counts from n\_applicants file

``` r
n_applicants %>% 
  gather(season, total_apps, `2017-18`:`2019-20`)
```

    ## # A tibble: 15 x 3
    ##    area          season  total_apps
    ##    <chr>         <chr>        <dbl>
    ##  1 Affective     2017-18        170
    ##  2 Cognitive     2017-18         77
    ##  3 Developmental 2017-18        130
    ##  4 Neuroscience  2017-18        101
    ##  5 Social        2017-18        232
    ##  6 Affective     2018-19        176
    ##  7 Cognitive     2018-19         62
    ##  8 Developmental 2018-19        181
    ##  9 Neuroscience  2018-19         73
    ## 10 Social        2018-19        248
    ## 11 Affective     2019-20        319
    ## 12 Cognitive     2019-20        127
    ## 13 Developmental 2019-20        282
    ## 14 Neuroscience  2019-20        141
    ## 15 Social        2019-20        358
