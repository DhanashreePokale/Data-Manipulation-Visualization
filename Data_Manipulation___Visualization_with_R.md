Data Manipulation Visualization on Diamonds Dataset
================

About Data
==========

Prices of 50,000 round cut diamonds

Description: A dataset containing the prices and other attributes of almost 54,000 diamonds. The variables are as follows:

Usage: diamonds

Format: A data frame with 53940 rows and 10 variables:

-   price: price in US dollars ($326–$18,823)
-   carat: weight of the diamond (0.2–5.01)
-   cut: quality of the cut (Fair, Good, Very Good, Premium, Ideal)
-   color: diamond colour, from J (worst) to D (best)
-   clarity: a measurement of how clear the diamond is (I1 (worst), SI1, SI2, VS1, VS2, VVS1, VVS2, IF (best))
-   x: length in mm (0–10.74)
-   y: width in mm (0–58.9)
-   z: depth in mm (0–31.8)
-   depth: total depth percentage = z / mean(x, y) = 2 \* z / (x + y) (43–79)
-   table: width of top of diamond relative to widest point (43–95)

``` r
library(ggplot2)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

Ideal Cut Diamomds
==================

Filter function of Dplyer for data manipulation
-----------------------------------------------

``` r
diamonds %>% filter(cut == "Ideal") -> Ideal_cut
Ideal_cut %>% filter(price>15000) -> high_price
Ideal_cut %>% filter(price>10000 & price<15000) -> medium_price
Ideal_cut %>% filter(price<10000) -> low_price
```

Diamond Dimensions
==================

Select function of dplyer
-------------------------

``` r
diamonds %>% select('x','y','z') -> diamond_dimensions
diamond_dimensions %>% filter(x>5 & y>50)
```

    ## # A tibble: 1 x 3
    ##       x     y     z
    ##   <dbl> <dbl> <dbl>
    ## 1  8.09  58.9  8.06

``` r
head(diamond_dimensions)
```

    ## # A tibble: 6 x 3
    ##       x     y     z
    ##   <dbl> <dbl> <dbl>
    ## 1  3.95  3.98  2.43
    ## 2  3.89  3.84  2.31
    ## 3  4.05  4.07  2.31
    ## 4  4.20  4.23  2.63
    ## 5  4.34  4.35  2.75
    ## 6  3.94  3.96  2.48

Diamond Color
=============

Summarize function of dplyer
----------------------------

``` r
diamonds %>% filter(color == "D") -> diamond_best_color
diamond_best_color %>% filter(clarity == "IF") -> diamond_best_clarity
diamond_best_clarity %>% summarise(mean_price = mean(price))
```

    ## # A tibble: 1 x 1
    ##   mean_price
    ##        <dbl>
    ## 1    8307.37

``` r
head(diamond_dimensions)
```

    ## # A tibble: 6 x 3
    ##       x     y     z
    ##   <dbl> <dbl> <dbl>
    ## 1  3.95  3.98  2.43
    ## 2  3.89  3.84  2.31
    ## 3  4.05  4.07  2.31
    ## 4  4.20  4.23  2.63
    ## 5  4.34  4.35  2.75
    ## 6  3.94  3.96  2.48

Visualization
=============

Univariate Distribution of Cut with BarPlot
-------------------------------------------

``` r
ggplot(data = diamonds, aes(x = cut)) + geom_bar(fill = "lightsalmon3") #all bars with same color
```

![](Data_Manipulation___Visualization_with_R_files/figure-markdown_github/unnamed-chunk-5-1.png)

``` r
ggplot(data =diamonds, aes(x= cut, fill=cut)) + geom_bar() #all bars with different color
```

![](Data_Manipulation___Visualization_with_R_files/figure-markdown_github/unnamed-chunk-6-1.png)

Bivariate Analysis - Price vs Carat & Price vs Length of diamond with scatter plot
----------------------------------------------------------------------------------

As carat size increases price of diamonds increases.

``` r
ggplot(data =diamonds, aes(y=price, x= carat)) + geom_point(col ="palegreen4") 
```

![](Data_Manipulation___Visualization_with_R_files/figure-markdown_github/unnamed-chunk-7-1.png)

As length of diamond increases price of diamonds increases.

``` r
ggplot(data =diamonds, aes(y=price, x= x)) + geom_point(col ="mediumorchid4") 
```

![](Data_Manipulation___Visualization_with_R_files/figure-markdown_github/unnamed-chunk-8-1.png)
