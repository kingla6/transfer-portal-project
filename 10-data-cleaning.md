R Notebook
================

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.4     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## Warning: package 'tibble' was built under R version 4.0.3

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(janitor)
```

    ## 
    ## Attaching package: 'janitor'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

``` r
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
transfer_portal <- read.csv('raw-data/transfers.csv') %>% clean_names()
```

# Clean and subset data from transfer portal

``` r
start_date <- '11/16/2020'
current_date <- '12/8/2020'

transfer_portal <- transfer_portal %>% 
  # change date columns to actual date objects, this will allow for filtering by date
  mutate(initiated_date = mdy(initiated_date),
         last_updated = mdy(last_updated)) %>% 
  # filter by date and athletes that did not withdraw
  filter(initiated_date >= mdy(start_date),
         student_status != 'Withdrawn')
```

# Write updated transfer data to csv

``` r
setwd("C:/Users/kingl/Desktop/Projects/football/transfer-portal-project/clean-data/")
write.csv(transfer_portal, file = paste0('transfer-portal-', mdy(current_date), '.csv'))
```
