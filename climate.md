Climate
================
Faith Igomodu
August 29, 2024

# Visiualizing Climate Change Data With ggplot2

Climate change is here and observing its trends using historical
tempeature data paints a daunting image of a future where live as we
know it is drastically different. To explore these trends through
visualization, obtained temperature data and studied it using ggplot2.
Average mean temperature, minimum temperature and maxiumum temperature
from the National Center for Environmental Information (NCEI) for
Richmond, Virgina (station number USW00013740) between 1983-2019 was
obtained.

## Install and load libraries

Expecting the time series dataset may contained missing values, Times
Series Missing Vlaue imputation in R (imputeTS) package is used to fill
in any missing data. The imputeTS pacakge uses state-of-the-art
imputation algorithm to replace missing values.

``` r
#install.packages("imputeTS", quiet = T)
```

``` r
library(ggplot2)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ lubridate 1.9.3     ✔ tibble    3.2.1
    ## ✔ purrr     1.0.2     ✔ tidyr     1.3.1
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(readr)
library(imputeTS)
```

    ## Warning: package 'imputeTS' was built under R version 4.4.1

    ## Registered S3 method overwritten by 'quantmod':
    ##   method            from
    ##   as.zoo.data.frame zoo

## Read dataset

Read, clean and sumarize the dataset.

``` r
df <-read_csv("3785897.csv")
```

    ## Rows: 37 Columns: 5
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): STATION
    ## dbl (4): DATE, TAVG, TMAX, TMIN
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(df)
```

    ## # A tibble: 6 × 5
    ##   STATION      DATE  TAVG  TMAX  TMIN
    ##   <chr>       <dbl> <dbl> <dbl> <dbl>
    ## 1 USW00013740  1983  57.8  68.1  47.6
    ## 2 USW00013740  1984  58.4  69.1  47.6
    ## 3 USW00013740  1985  59.2  70.2  48.3
    ## 4 USW00013740  1986  58.8  69.3  48.2
    ## 5 USW00013740  1987  57.9  68.9  47  
    ## 6 USW00013740  1988  57.1  68.4  45.7

``` r
summary(df)
```

    ##    STATION               DATE           TAVG            TMAX      
    ##  Length:37          Min.   :1983   Min.   :56.60   Min.   :66.30  
    ##  Class :character   1st Qu.:1992   1st Qu.:58.10   1st Qu.:68.70  
    ##  Mode  :character   Median :2001   Median :59.10   Median :69.70  
    ##                     Mean   :2001   Mean   :59.09   Mean   :69.59  
    ##                     3rd Qu.:2010   3rd Qu.:59.90   3rd Qu.:70.60  
    ##                     Max.   :2019   Max.   :61.10   Max.   :72.30  
    ##       TMIN      
    ##  Min.   :45.70  
    ##  1st Qu.:47.60  
    ##  Median :48.70  
    ##  Mean   :48.57  
    ##  3rd Qu.:49.60  
    ##  Max.   :50.60
