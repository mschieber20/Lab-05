Lab 04 - La Quinta is Spanish for next to Denny’s, Pt. 2
================
Marq Schieber
2/27/2022

### Load packages and data

``` r
library(tidyverse) 
```

    ## Warning: package 'tidyr' was built under R version 4.0.5

    ## Warning: package 'readr' was built under R version 4.0.5

    ## Warning: package 'dplyr' was built under R version 4.0.5

``` r
library(dsbox) 
```

``` r
states <- read_csv("data/states.csv")
```

### Exercise 1 Filter the Denny’s dataframe for Alaska (AK) and save the result as dn_ak. How many Denny’s locations are there in Alaska?

``` r
dn_ak <- dennys %>%
  filter(state == "AK")
nrow(dn_ak)
```

    ## [1] 3

There are 3

### Exercise 2 Filter the La Quinta dataframe for Alaska (AK) and save the result as lq_ak. How many La Quinta locations are there in Alaska?

``` r
lq_ak <- laquinta %>%
  filter(state == "AK")
nrow(lq_ak)
```

    ## [1] 2

There are 2.

### Exercise 3 How many pairings are there between all Denny’s and all La Quinta locations in Alaska, i.e., how many distances do we need to calculate between the locations of these establishments in Alaska?

There are 6 pairings.

``` r
dn_lq_ak <- full_join(dn_ak, lq_ak, by = "state")
dn_lq_ak
```

    ## # A tibble: 6 × 11
    ##   address.x     city.x state zip.x longitude.x latitude.x address.y city.y zip.y
    ##   <chr>         <chr>  <chr> <chr>       <dbl>      <dbl> <chr>     <chr>  <chr>
    ## 1 2900 Denali   Ancho… AK    99503       -150.       61.2 3501 Min… "\nAn… 99503
    ## 2 2900 Denali   Ancho… AK    99503       -150.       61.2 4920 Dal… "\nFa… 99709
    ## 3 3850 Debarr … Ancho… AK    99508       -150.       61.2 3501 Min… "\nAn… 99503
    ## 4 3850 Debarr … Ancho… AK    99508       -150.       61.2 4920 Dal… "\nFa… 99709
    ## 5 1929 Airport… Fairb… AK    99701       -148.       64.8 3501 Min… "\nAn… 99503
    ## 6 1929 Airport… Fairb… AK    99701       -148.       64.8 4920 Dal… "\nFa… 99709
    ## # … with 2 more variables: longitude.y <dbl>, latitude.y <dbl>

### Exercise 4 How many observations are in the joined dn_lq_ak data frame? What are the names of the variables in this data frame.

There are 6 observations in the joined data frame.

Variable names: adress, city, state, zip, long., lat., address.

### Exercise 5 What function from the tidyverse do we use the add a new variable to a data frame while keeping the existing variables?

``` r
haversine <- function(long1, lat1, long2, lat2, round = 3) {
  # convert to radians
  long1 = long1 * pi / 180
  lat1  = lat1  * pi / 180
  long2 = long2 * pi / 180
  lat2  = lat2  * pi / 180
  
  R = 6371 # Earth mean radius in km
  
  a = sin((lat2 - lat1)/2)^2 + cos(lat1) * cos(lat2) * sin((long2 - long1)/2)^2
  d = R * 2 * asin(sqrt(a))
  
  return( round(d,round) ) # distance in km
}
```

…

### Exercise 6

…

Add exercise headings as needed.
