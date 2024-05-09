Introduction to R with Tidyverse
================
Sophie Lee
2024-05-09

- [Chapter 7: Data preparation and
  manipulation](#chapter-7-data-preparation-and-manipulation)
  - [7.1 Combining multiple datasets](#71-combining-multiple-datasets)
  - [7.2 Transforming data](#72-transforming-data)
  - [7.3 Summary tables](#73-summary-tables)
  - [Exercise 4](#exercise-4)

## Chapter 7: Data preparation and manipulation

### 7.1 Combining multiple datasets

We may wish to combine and use data from different files within R. For
example, in our case we have the core spending power for each year
between 2015 and 2020. First, we must read each dataset into R and save
them as objects. We could use the `read_csv` function for each file
separately and create a data frame for each year:

``` r
CSP_2015 <- read_csv("data/CSP_2015.csv")

CSP_2016 <- read_csv("data/CSP_2016.csv")
```

We can then combine columns from these datasets by joining them using
variables which are shared between them. In this case, each local
authority has a unique ONS code and naming variable, they also have a
region variable which we can include within the join.

In Tidyverse, there is a family of ‘joining’ functions that combine two
datasets at a time. The choice of function depends on which observations
we wish to keep where the joining variables do not match between data.
In this example, all local authorities are the same across each year, so
we will use `full_join`.

``` r
csp_201516 <- full_join(CSP_2015, CSP_2016, 
                        by = c("ons_code", "authority", "region"))
```

The alternatives to `full_join` include `inner_join`, which only returns
a dataset with observations contained in both objects, `left_join`,
where all observations are returned from the first object, whether they
are in the second or not, and `right_join`. where all observations from
the second object are returned, whether or not they are in the first.

Joining functions are useful when combining two objects but requires
repetition when joining more than two. To combine all 6 core spending
power datasets from 2015 to 2020 in this way would require a lot of
code. Instead, we can automate this process by using **functional
programming** included in the `purrr` package.

The first step requires reading in all csv files by repeatedly applying
`read_csv`. This requires a list of file names from the working
directory. The function `list.files` introduced earlier contains an
optional argument, `pattern` which can be used to return files and
folders that match a naming pattern. In this case, all csv files begin
“CSP_20”, so to return this list of names from the *data* folder, we use
the function:

``` r
list.files(path = "data", pattern = "CSP_20")
```

    ## [1] "CSP_2015.csv" "CSP_2016.csv" "CSP_2017.csv" "CSP_2018.csv" "CSP_2019.csv"
    ## [6] "CSP_2020.csv"

Next, we must apply `read_csv` to each element of the list of file
names. The function `map` allows us to do this and return a list of
tibbles (datasets). As the data lies in a folder in the working
directory, we must add this file path to the file names:

``` r
list.files(path = "data", pattern = "CSP_20") %>% 
  paste0("data/", .) %>% 
  map(read_csv)
```

Finally, we require a function that apply `full_join` iteratively to
this list of tibbles to reduce it to a single tibble containing core
spending powers for all years. The function that does this is `reduce`:

``` r
csp_201520 <- list.files(path = "data", pattern = "CSP_20") %>% 
  paste0("data/", .) %>% 
  map(read_csv) %>% 
  reduce(full_join, by = c("ons_code", "authority", "region"))
```

``` r
str(csp_201520)
```

    ## spc_tbl_ [396 × 39] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ ons_code        : chr [1:396] "E07000223" "E07000026" "E07000032" "E07000224" ...
    ##  $ authority       : chr [1:396] "Adur" "Allerdale" "Amber Valley" "Arun" ...
    ##  $ region          : chr [1:396] "SE" "NW" "EM" "SE" ...
    ##  $ sfa_2015        : num [1:396] 3.02 5.81 5.3 6.15 6.27 ...
    ##  $ under_index_2015: num [1:396] 0.0234 0.0484 0.0427 0.0486 0.0514 ...
    ##  $ ct_total_2015   : num [1:396] 5.47 4.54 5.65 9.16 5.29 ...
    ##  $ nhb_2015        : num [1:396] 0.652 1.068 1.431 3.088 2.518 ...
    ##  $ nhb_return_2015 : num [1:396] 0.00523 0.0107 0.00947 0.01083 0.0114 ...
    ##  $ rsdg_2015       : num [1:396] 0 0.0623 0 0 0 ...
    ##  $ sfa_2016        : num [1:396] 2.39 5.05 4.5 5.02 5.42 ...
    ##  $ under_index_2016: num [1:396] 0.0234 0.0484 0.0427 0.0486 0.0514 ...
    ##  $ ct_total_2016   : num [1:396] 5.68 4.71 5.69 9.61 5.6 ...
    ##  $ nhb_2016        : num [1:396] 0.767 1.526 1.813 4.014 3.088 ...
    ##  $ nhb_return_2016 : num [1:396] 0.00374 0.00765 0.00678 0.00774 0.00816 ...
    ##  $ rsdg_2016       : num [1:396] 0 0.324 0 0 0 ...
    ##  $ sfa_2017        : num [1:396] 1.92 4.47 3.89 4.18 4.78 ...
    ##  $ under_index_2017: num [1:396] 0.0248 0.0513 0.0452 0.0515 0.0545 ...
    ##  $ ct_total_2017   : num [1:396] 5.85 4.92 5.99 10.18 5.87 ...
    ##  $ nhb_2017        : num [1:396] 0.553 1.604 1.628 3.677 2.577 ...
    ##  $ nhb_return_2017 : num [1:396] 0.00397 0.00812 0.00719 0.00821 0.00865 ...
    ##  $ rsdg_2017       : num [1:396] 0 0.261 0 0 0 ...
    ##  $ sfa_2018        : num [1:396] 1.7 4.17 3.57 3.72 4.43 ...
    ##  $ under_index_2018: num [1:396] 0.039 0.0806 0.071 0.0809 0.0856 ...
    ##  $ ct_total_2018   : num [1:396] 6.08 5.1 6.33 10.65 6.15 ...
    ##  $ nhb_2018        : num [1:396] 0.202 1.004 1.359 2.733 2.086 ...
    ##  $ nhb_return_2018 : num [1:396] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ rsdg_2018       : num [1:396] 0 0.326 0 0 0 ...
    ##  $ sfa_2019        : num [1:396] 1.74 3.79 3.18 3.61 4.02 ...
    ##  $ under_index_2019: num [1:396] 0.0567 0.1172 0.1033 0.1176 0.1246 ...
    ##  $ ct_total_2019   : num [1:396] 6.35 5.3 6.58 11.13 6.22 ...
    ##  $ nhb_2019        : num [1:396] 0.126 0.838 1.489 2.664 1.608 ...
    ##  $ nhb_return_2019 : num [1:396] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ rsdg_2019       : num [1:396] 0 0.326 0 0 0 ...
    ##  $ sfa_2020        : num [1:396] 1.77 3.85 3.23 3.67 4.08 ...
    ##  $ under_index_2020: num [1:396] 0.0708 0.1465 0.1292 0.147 0.1557 ...
    ##  $ ct_total_2020   : num [1:396] 6.53 5.4 6.85 11.61 6.42 ...
    ##  $ nhb_2020        : num [1:396] 0.0881 0.6061 1.5786 2.2949 1.1547 ...
    ##  $ nhb_return_2020 : num [1:396] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ rsdg_2020       : num [1:396] 0 0.326 0 0 0 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   ons_code = col_character(),
    ##   ..   authority = col_character(),
    ##   ..   region = col_character(),
    ##   ..   sfa_2015 = col_double(),
    ##   ..   under_index_2015 = col_double(),
    ##   ..   ct_total_2015 = col_double(),
    ##   ..   nhb_2015 = col_double(),
    ##   ..   nhb_return_2015 = col_double(),
    ##   ..   rsdg_2015 = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

### 7.2 Transforming data

The dataset created above is currently in what is known as **wide
format**, this means there is a variable per measure per year. However,
for some analyses and visualisations, we may wish to convert this
dataset into **long format**, where each row is an observation per year.
To convert data between wide and long formats, we can use the Tidyverse
functions `pivot_longer()` and `pivot_wider()`.

The first argument required by \``pivot_longer` is the data object we
wish to transform. This is followed by the columns we wish to pivot (in
this case, all variable other than the local authority codes, names, and
regions). The next steps will depend on the type of data we wish to
transform, the values we want to extract, and the variable names
themselves. For more examples, type `vignette("pivot")` into the R
console.

In this example, we wish to create a row per year and a variable for
each stream of funding. Each of the variable names begin with the stream
acronym, followed by an underscore and the year. We can break these
variables up by specifying multiple column names using the `names_to`
argument. In this case, the name is taken from the first part of the
original variable name (R reads this as `.value`), we also want a new
variable called *year*. The argument `names_pattern` tells R which part
of the original variable names relate to which variable specified in
`names_to` (defined within `()`):

``` r
csp_long <- pivot_longer(csp_201520, 
                           cols = sfa_2015:rsdg_2020,
                           names_to = c(".value", "year"),
                           names_pattern = "(.*)_(.*)")
```

Our new dataframe has one row per local authority per year and a
variable for each of the spending streams. We may wish to calculate the
total core spending for each local authority per year and include this
as a new variable, `total_spend`, within the data:

``` r
csp_long2 <- mutate(csp_long, 
                      total_spend = sfa + under_index + ct_total + nhb + 
                         nhb_return + rsdg)
```

### 7.3 Summary tables

The function `summarise` allows us to create summary tables from data
objects. Without combining `summarise` with any other functions, this
will compress a data object into a tibble with a single row and a
variable per summary. Summary functions that are compatible with
`summarise` include `mean, median, quantile, sum, min, max`. Another
useful summary is `n()` which returns the number of rows the summaries
have been calculated over. For a full list of compatible summary
functions, view the helpfile `?summarise`.

If we wanted to summarise the total core spending power between 2015 and
2020 across all local authorities, we can apply `summarise` to the long
format data from the previous section:

``` r
summarise(csp_long2, 
          total_spend_all = sum(total_spend),
          mean_total_spend = mean(total_spend),
          median_total_spend = median(total_spend),
          quantile10_total_spend = quantile(total_spend, 0.1),
          total_obs = n())
```

    ## # A tibble: 1 × 5
    ##   total_spend_all mean_total_spend median_total_spend quantile10_total_spend
    ##             <dbl>            <dbl>              <dbl>                  <dbl>
    ## 1         263484.             111.               17.6                   8.34
    ## # ℹ 1 more variable: total_obs <int>

Combining `summarise` with a grouping function, `group_by` provides
grouped summaries of the data. For example, is we wished to produce a
summary table with a row per local authority, summarising the total
spending between 2015 and 2020, we would use the following:

``` r
csp_long2 %>% 
group_by(ons_code, authority) %>% 
    summarise(total_spend_all = sum(total_spend),
              mean_total_spend = mean(total_spend),
          median_total_spend = median(total_spend),
          quantile10_total_spend = quantile(total_spend, 0.1),
          total_obs = n()) %>%
    ungroup()
```

    ## `summarise()` has grouped output by 'ons_code'. You can override using the
    ## `.groups` argument.

    ## # A tibble: 396 × 7
    ##    ons_code  authority       total_spend_all mean_total_spend median_total_spend
    ##    <chr>     <chr>                     <dbl>            <dbl>              <dbl>
    ##  1 -         Greater London…          12416.           2069.              2022. 
    ##  2 E06000001 Hartlepool                 485.             80.8               80.3
    ##  3 E06000002 Middlesbrough              711.            119.               118. 
    ##  4 E06000003 Redcar And Cle…            660.            110.               109. 
    ##  5 E06000004 Stockton-on-Te…            832.            139.               138. 
    ##  6 E06000005 Darlington                 474.             79.0               78.5
    ##  7 E06000006 Halton                     598.             99.7               99.0
    ##  8 E06000007 Warrington                 806.            134.               133. 
    ##  9 E06000008 Blackburn with…            692.            115.               115. 
    ## 10 E06000009 Blackpool                  750.            125.               124. 
    ## # ℹ 386 more rows
    ## # ℹ 2 more variables: quantile10_total_spend <dbl>, total_obs <int>

When producing grouped summaries, it is important to ungroup the data
after the function has been performed using the `ungroup` function.
Failure to do this keeps the grouping structure in the object which can
slow down future analysis, or can interact with future analyses and
produce invalid results.

### Exercise 4

1.  Create a data frame with the minimum, maximum and median total spend
    per year for each region.
2.  Produce a frequency table containing the number and percentage of
    local authorities in each region.
3.  Convert the data object `csp_long2` back into wide format, with one
    row per local authority and one variable per total spend per year
    (HINT: start by selecting only the variables you need from the long
    data frame). Use the help file `?pivot_wider` and
    `vignette("pivot")` for more hints.
4.  Using your new wide data frame, calculate the difference in total
    spending for each local authority between 2015 and 2020. How many
    local authorities have had an overall reduction in spending since
    2015?
