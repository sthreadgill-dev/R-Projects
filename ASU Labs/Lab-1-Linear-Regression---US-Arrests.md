Lab 1 - Linear Regression - US Arrests
================
Susan Threadgill
2025-08-27

# M1 Lab 1 Submission

# Overview

In this assignment, you will analyze the **USArrests** dataset, which
contains statistics on violent crime rates in the United States for each
of the 50 states in 1973. You will apply the R skills you learned in
this module, including importing data, summarizing information, creating
visualizations, and using tidyverse functions.

# Load Libraries

For this assignment, and most others in this class you will need to use
the `tidyverse` and `GGally` libraries. Before loading your libraries,
if you have not already installed those libraries on the version of R
you are currently using, please install them now. You can do that by
typing the code below in your console or by using the Tools dropdown
menu. You will not need to do this again for future assignments as long
as you are using the same computer.

``` r
install.packages("tidyverse")
install.packages("GGally")
```

Load the necessary libraries for data analysis and visualization.

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.2     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(GGally)  # For pairwise scatter plots
```

# Data Access

The **USArrests** dataset contains the following variables: - `Murder`:
Murder arrests (per 100,000 residents) - `Assault`: Assault arrests (per
100,000 residents) - `UrbanPop`: Percent of the population living in
urban areas

``` r
# Read in dataset
us_arrests <- read_csv("M1-US-Arrests-Data.csv")
```

    ## Rows: 50 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): State
    ## dbl (3): Murder, Assault, UrbanPop
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Use the following commands to explore the dataset content:

``` r
# View first few rows of the dataset
head(us_arrests)
```

    ## # A tibble: 6 × 4
    ##   State      Murder Assault UrbanPop
    ##   <chr>       <dbl>   <dbl>    <dbl>
    ## 1 Alabama      13.2     236       58
    ## 2 Alaska       10       263       48
    ## 3 Arizona       8.1     294       80
    ## 4 Arkansas      8.8     190       50
    ## 5 California    9       276       91
    ## 6 Colorado      7.9     204       78

``` r
# Get a quick glimpse of the dataset
glimpse(us_arrests)
```

    ## Rows: 50
    ## Columns: 4
    ## $ State    <chr> "Alabama", "Alaska", "Arizona", "Arkansas", "California", "Co…
    ## $ Murder   <dbl> 13.2, 10.0, 8.1, 8.8, 9.0, 7.9, 3.3, 5.9, 15.4, 17.4, 5.3, 2.…
    ## $ Assault  <dbl> 236, 263, 294, 190, 276, 204, 110, 238, 335, 211, 46, 120, 24…
    ## $ UrbanPop <dbl> 58, 48, 80, 50, 91, 78, 77, 72, 80, 60, 83, 54, 83, 65, 57, 6…

# Question 1

Use the following tasks to practice subsetting data using `filter()` to
select specific rows and `select()` to choose specific columns.

## 1.1

Retrieve all rows where `Murder` is greater than 10 per 100,000
residents.

``` r
# Your answer here
us_arrests %>%   
  filter(Murder > 10) %>% 
  head(5)
```

    ## # A tibble: 5 × 4
    ##   State     Murder Assault UrbanPop
    ##   <chr>      <dbl>   <dbl>    <dbl>
    ## 1 Alabama     13.2     236       58
    ## 2 Florida     15.4     335       80
    ## 3 Georgia     17.4     211       60
    ## 4 Illinois    10.4     249       83
    ## 5 Louisiana   15.4     249       66

## 1.2

Retrieve all rows where `UrbanPop` is less than 50%.

``` r
# Your answer here
us_arrests %>% 
  filter(UrbanPop < 50) %>% 
  head(5)
```

    ## # A tibble: 5 × 4
    ##   State          Murder Assault UrbanPop
    ##   <chr>           <dbl>   <dbl>    <dbl>
    ## 1 Alaska           10       263       48
    ## 2 Mississippi      16.1     259       44
    ## 3 North Carolina   13       337       45
    ## 4 North Dakota      0.8      45       44
    ## 5 South Carolina   14.4     279       48

## 1.3

Find the data for the states of **California, Texas, and New York**.

``` r
# Your answer here
us_arrests %>% 
  filter(State %in% c("California", "Texas", "New York")) %>% 
  select(State, Murder, Assault, UrbanPop)
```

    ## # A tibble: 3 × 4
    ##   State      Murder Assault UrbanPop
    ##   <chr>       <dbl>   <dbl>    <dbl>
    ## 1 California    9       276       91
    ## 2 New York     11.1     254       86
    ## 3 Texas        12.7     201       80

## 1.4

Select only the `State` and `Murder` columns.

``` r
# Your answer here
us_arrests %>% 
  select(State, Murder) %>% 
  head(5)
```

    ## # A tibble: 5 × 2
    ##   State      Murder
    ##   <chr>       <dbl>
    ## 1 Alabama      13.2
    ## 2 Alaska       10  
    ## 3 Arizona       8.1
    ## 4 Arkansas      8.8
    ## 5 California    9

## 1.5

Select the `State`, `Assault`, and `UrbanPop` columns.

``` r
# Your answer here
us_arrests %>% 
  select(State, Assault, UrbanPop) %>% 
  head(5)
```

    ## # A tibble: 5 × 3
    ##   State      Assault UrbanPop
    ##   <chr>        <dbl>    <dbl>
    ## 1 Alabama        236       58
    ## 2 Alaska         263       48
    ## 3 Arizona        294       80
    ## 4 Arkansas       190       50
    ## 5 California     276       91

## 1.6

Retrieve only the states where `Assault` is greater than 200, but
display only the `State` and `Assault` columns.

``` r
# Your answer here
us_arrests %>% 
  filter(Assault > 200) %>% 
  select(State, Assault) %>% 
  head(5)
```

    ## # A tibble: 5 × 2
    ##   State      Assault
    ##   <chr>        <dbl>
    ## 1 Alabama        236
    ## 2 Alaska         263
    ## 3 Arizona        294
    ## 4 California     276
    ## 5 Colorado       204

## 1.7

Retrieve only the states where `Murder` is below 5 and `UrbanPop` is
above 70, but display only `State`, `Murder`, and `UrbanPop`.

``` r
# Your answer here
us_arrests %>% 
  filter(Murder <5 & UrbanPop >70) %>% 
  select(State, Murder, UrbanPop) 
```

    ## # A tibble: 5 × 3
    ##   State         Murder UrbanPop
    ##   <chr>          <dbl>    <dbl>
    ## 1 Connecticut      3.3       77
    ## 2 Massachusetts    4.4       85
    ## 3 Rhode Island     3.4       87
    ## 4 Utah             3.2       80
    ## 5 Washington       4         73

# Question 2

Create a new variable `high_murder` that equals **1** if `Murder` is
greater than the median murder rate and **0** otherwise.

``` r
# Your answer here
median_murder_rate <- median(us_arrests$Murder)
high_murder <- ifelse(us_arrests$Murder > median_murder_rate, 1, 0)
```

# Question 3

## 3.1

Create a scatter plot to show the relationship between the number of
assault arrests (`Assault`) and murder arrests (`Murder`).

``` r
# Your answer here
ggplot(us_arrests, aes(x = Assault, y = Murder)) +
 geom_point(alpha = 0.6, color = "navyblue") +
 labs(title = "Murder vs Assault Arrests by State (per 100,000 residents)", x = "Assault Arrests", y = "Murder Arrests") +
  theme(plot.title = element_text(hjust = 0.5, margin = margin(t = 10, b = 10)),
        axis.title.x = element_text(hjust = 0.5,margin = margin(t = 10, b = 10)),  
        axis.title.y = element_text(hjust = 0.5,margin = margin(r = 10, l = 10)))
```

![](Lab-1-Linear-Regression---US-Arrests_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

## 3.2

Add a linear trend line to the plot.

``` r
# Your answer here
ggplot(us_arrests, aes(x = Assault, y = Murder)) +
 geom_point(alpha = 0.6, color = "navyblue") +
 labs(title = "Murder vs Assault Arrests by State (per 100,000 residents)", x = "Assault Arrests", y = "Murder Arrests") +
 geom_smooth(method = "lm", se = FALSE, color = "red4") +
theme(plot.title = element_text(hjust = 0.5, margin = margin(t = 10, b = 10)),
        axis.title.x = element_text(hjust = 0.5,margin = margin(t = 10, b = 10)),  
        axis.title.y = element_text(hjust = 0.5,margin = margin(r = 10, l = 10)))
```

    ## `geom_smooth()` using formula = 'y ~ x'

![](Lab-1-Linear-Regression---US-Arrests_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

## 3.3

Create histograms for `Murder` and `UrbanPop` to understand their
distributions.

``` r
# Your answer here for Murder
range_min <- min(us_arrests$Murder)
range_max <- max(us_arrests$Murder)

ggplot(us_arrests, aes(x = Murder)) +
  geom_histogram(binwidth = 1, boundary = 0, closed = "left", fill = "navyblue", color = "black", alpha = 0.7) +
    scale_x_continuous(limits = c(0, NA), breaks = seq(0, 20, by = 1)) +
  labs(x = "Murder Arrests (per 100k residents)", y = "Count of States") +
  ggtitle("State-Level Murder Arrests") +
  theme(plot.title = element_text(hjust = 0.5, margin = margin(t = 10, b = 10)),
        axis.title.x = element_text(hjust = 0.5,margin = margin(t = 10, b = 10)),  
        axis.title.y = element_text(hjust = 0.5,margin = margin(r = 10, l = 10)))
```

![](Lab-1-Linear-Regression---US-Arrests_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
# Your answer here for UrbanPop
ggplot(us_arrests, aes(x = UrbanPop)) +
  geom_histogram(binwidth = 5, boundary = 0, closed = "left", fill = "darkslateblue", color = "black", alpha = 0.7) +
  scale_x_continuous(limits = c(30, NA), breaks = seq(0, 100, by = 10))+
  labs(title = "% of the population living in urban areas", x = "Urban Population %", y = "Count of States") +
 theme(plot.title = element_text(hjust = 0.5, margin = margin(t = 10, b = 10)),
        axis.title.x = element_text(hjust = 0.5,margin = margin(t = 10, b = 10)),  
        axis.title.y = element_text(hjust = 0.5,margin = margin(r = 10, l = 10)))
```

![](Lab-1-Linear-Regression---US-Arrests_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

## 3.4

Generate pairwise scatter plots to explore relationships among `Murder`,
`Assault`, and `UrbanPop`.

``` r
# Your answer here
ggpairs( 
  us_arrests[, c("Murder", "Assault", "UrbanPop")],
  title = "Pairwise Scatter Plots: Murder, Assault, and Urban Population",
  upper = list(continuous = wrap("cor", size = 4, color = "red4")),   
  lower = list(continuous = function(data, mapping, ...) {
      ggplot(data, mapping) +
        geom_point(color = "slateblue", alpha = 0.6) +       
        geom_smooth(method = "lm", se = FALSE, color = "red4", linewidth = 0.5, alpha = 0.7) 
    }),  
  diag  = list(continuous = wrap("densityDiag", fill = "darkseagreen")),
  labeller = as_labeller(c(
    Murder   = "Murder",
    Assault  = "Assault",
    UrbanPop = "Urban Pop"))
) +
  theme(
    plot.title = element_text(hjust = 0.5, margin = margin(t = 10, b = 10))
  )
```

    ## `geom_smooth()` using formula = 'y ~ x'
    ## `geom_smooth()` using formula = 'y ~ x'
    ## `geom_smooth()` using formula = 'y ~ x'

![](Lab-1-Linear-Regression---US-Arrests_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

# Question 4

## 4.1

Calculate the mean murder rate for states classified as `high_murder`
(1) and not high murder (0).

``` r
# Your answer here
mean(us_arrests$Murder[high_murder == 1])
```

    ## [1] 11.4

``` r
mean(us_arrests$Murder[high_murder == 0])
```

    ## [1] 4.176

## 4.2

Create a new variable `high_urban` that equals **1** if `UrbanPop` is
greater than the median urban population percentage and **0** otherwise.
Then, summarize the mean murder rate by `high_urban`.

``` r
# Your answer here
median_urban_pop <- median(us_arrests$UrbanPop)
high_urban <- ifelse(us_arrests$UrbanPop > median_urban_pop, 1, 0)

us_arrests %>% 
  transmute(high_urban, Murder) %>% 
  group_by(high_urban) %>% 
  summarise(mean_murder = mean(Murder))
```

    ## # A tibble: 2 × 2
    ##   high_urban mean_murder
    ##        <dbl>       <dbl>
    ## 1          0        7.57
    ## 2          1        8.02
