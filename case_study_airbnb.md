Case Study: NYC Airbnb Data
================
Jessica Lavery
10/8/2019

``` r
# get airbnb dataset from p8105.datasets package
data(nyc_airbnb)

# look at structure of airbnb data
str(nyc_airbnb)
```

    ## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame': 40753 obs. of  17 variables:
    ##  $ id                            : num  7949480 16042478 1886820 6627449 5557381 ...
    ##  $ review_scores_location        : num  10 NA NA 10 10 10 10 9 10 9 ...
    ##  $ name                          : chr  "City Island Sanctuary relaxing BR & Bath w Parking" "WATERFRONT STUDIO APARTMENT" "Quaint City Island Community." "Large 1 BDRM in Great location" ...
    ##  $ host_id                       : num  119445 9117975 9815788 13886510 28811542 ...
    ##  $ host_name                     : chr  "Linda & Didier" "Collins" "Steve" "Arlene" ...
    ##  $ neighbourhood_group           : chr  "Bronx" "Bronx" "Bronx" "Bronx" ...
    ##  $ neighbourhood                 : chr  "City Island" "City Island" "City Island" "City Island" ...
    ##  $ lat                           : num  -73.8 -73.8 -73.8 -73.8 -73.8 ...
    ##  $ long                          : num  40.9 40.9 40.8 40.8 40.9 ...
    ##  $ room_type                     : chr  "Private room" "Private room" "Entire home/apt" "Entire home/apt" ...
    ##  $ price                         : num  99 200 300 125 69 125 85 39 95 125 ...
    ##  $ minimum_nights                : num  1 7 7 3 3 2 1 2 3 2 ...
    ##  $ number_of_reviews             : num  25 0 0 12 86 41 74 114 5 206 ...
    ##  $ last_review                   : Date, format: "2017-04-23" NA ...
    ##  $ reviews_per_month             : num  1.59 NA NA 0.54 3.63 2.48 5.43 2.06 5 2.98 ...
    ##  $ calculated_host_listings_count: num  1 1 1 1 1 1 1 4 3 4 ...
    ##  $ availability_365              : num  170 180 365 335 352 129 306 306 144 106 ...

``` r
nyc_airbnb %>%
  count(room_type)
```

    ## # A tibble: 3 x 2
    ##   room_type           n
    ##   <chr>           <int>
    ## 1 Entire home/apt 19937
    ## 2 Private room    19626
    ## 3 Shared room      1190

``` r
nyc_airbnb %>%
  count(neighbourhood_group)
```

    ## # A tibble: 5 x 2
    ##   neighbourhood_group     n
    ##   <chr>               <int>
    ## 1 Bronx                 649
    ## 2 Brooklyn            16810
    ## 3 Manhattan           19212
    ## 4 Queens               3821
    ## 5 Staten Island         261

Potential questions:  
1\. How are airbnb prices related to rent in the neighborhood?  
2\. Which neighborhoods have the most and least expensive rentals?  
3\. Do hosts with multiple sites have higher prices or ratings than
hosts with one site? 4. Does price have any relation to ratings? 5. Does
price drive availability? 6. Does room type correspond to ratings? Does
this differ by neighborhoods?

### How are airbnb prices related to rent in the neighborhood?

``` r
nyc_airbnb %>% 
  group_by(neighbourhood_group) %>% 
  summarize(mean_price = mean(price),
            sd_price = sd(price)) %>% 
  kable()
```

<table>

<thead>

<tr>

<th style="text-align:left;">

neighbourhood\_group

</th>

<th style="text-align:right;">

mean\_price

</th>

<th style="text-align:right;">

sd\_price

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

Bronx

</td>

<td style="text-align:right;">

82.82897

</td>

<td style="text-align:right;">

77.33373

</td>

</tr>

<tr>

<td style="text-align:left;">

Brooklyn

</td>

<td style="text-align:right;">

119.67704

</td>

<td style="text-align:right;">

184.09206

</td>

</tr>

<tr>

<td style="text-align:left;">

Manhattan

</td>

<td style="text-align:right;">

180.09338

</td>

<td style="text-align:right;">

238.17625

</td>

</tr>

<tr>

<td style="text-align:left;">

Queens

</td>

<td style="text-align:right;">

94.72939

</td>

<td style="text-align:right;">

122.65699

</td>

</tr>

<tr>

<td style="text-align:left;">

Staten Island

</td>

<td style="text-align:right;">

128.01916

</td>

<td style="text-align:right;">

332.66042

</td>

</tr>

</tbody>

</table>
