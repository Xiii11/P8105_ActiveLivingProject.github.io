final
================

loading necessary package

``` r
library(tidyverse)
library(ggplot2)
```

import commuting dataset

``` r
commuting_df = 
  read.csv("data/commuting.csv", na = c("NA",".","")) |> 
   janitor::clean_names()
```

transfer datatype to numeric

``` r
commute_df = commuting_df |> 
  mutate(across(c(bicycle_number, car_truck_or_van_number, public_transportation_number, walked_number),
                ~as.numeric(gsub(",", "", .))))
```

data explore

``` r
summary_data = commute_df |> 
  group_by(geography) |> 
  summarise(
    Total_Bicycle = sum(bicycle_number, na.rm = TRUE),
    Total_Car = sum(car_truck_or_van_number, na.rm = TRUE),
    Total_Public_Transport = sum(public_transportation_number, na.rm = TRUE),
    Total_Walked = sum(walked_number, na.rm = TRUE)
  )
```
