Introduction to R with Tidyverse
================
Sophie Lee
2024-05-10

- [Chapter 5: R packages and add-ons](#chapter-5-r-packages-and-add-ons)
- [Chapter 6: Introduction to the Tidyverse and data
  wrangling](#chapter-6-introduction-to-the-tidyverse-and-data-wrangling)
  - [6.1 Tidyverse](#61-tidyverse)
  - [6.2 The working directory](#62-the-working-directory)
  - [6.3 Data input](#63-data-input)
  - [6.4 Selecting variables](#64-selecting-variables)
  - [6.5 Filtering data](#65-filtering-data)
  - [6.6 Pipes](#66-pipes)
  - [6.7 Adding new variables](#67-adding-new-variables)
- [Exercise 3](#exercise-3)

## Chapter 5: R packages and add-ons

R packages are a collection of functions and datasets developed by R
users that expand existing base R capabilities or add completely new
ones. Packages allow users to apply the most up-to-date methods shortly
after they are developed, unlike other statistical software packages
that require an entirely new version. The quickest way to install a
package in R is:

`install.packages(‘name of package’)`

R requires an internet connection to install a package from R’s online
repository, CRAN. Packages must be downloaded before their first use on
a machine and to install any updates that have been made since the last
installation.

Once a package has been installed, use the following code to load it
into your R session:

`require(name of package)`

or

`library(name of package)`

Packages must be reloaded every time a new session of R is opened.
Therefore, it is good practice to include the `require` or `library`
command at the beginning of a script file.

All available packages are listed on the [CRAN
website](https://cran.r-project.org/web/packages/available_packages_by_name.html)
with details of what each one does. Use the `installed.packages( )` for
a list of all installed packages on your machine.

## Chapter 6: Introduction to the Tidyverse and data wrangling

### 6.1 Tidyverse

Up to this point in the course, we have been using a style of R coding
language (or syntax) known as base R, the original version of the
language that does not require any additional packages. However, there
are different approaches that have been developed within R packages. For
example, the Tidyverse set of packages, which aim to improve certain
aspects of R syntax.

The choice of syntax style depends on personal preference. Base R is
very stable as it is not dependent on packages which may be updated
regularly. However, the Tidyverse set of packages have been developed to
make R code more readable and flexible than base R. We will be using a
combination of base R and Tidyverse coding style within this course to
utilise the extensive data manipulation tools developed for Tidyverse.

To load tidyverse packages into your R session, run the following code:

``` r
install.packages(‘tidyverse') 
```

``` r
library(tidyverse) 
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.2     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.1     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the ]8;;http://conflicted.r-lib.org/conflicted package]8;; to force all conflicts to become errors

### 6.2 The working directory

The working directory is a file path on your computer that R sets as the
default location when opening, saving, or exporting documents, files,
and graphics. It is possible to specify this location manually but
setting the working directory saves time and makes code more efficient.

To set the working directory, choose *Session -\> Set Working Directory
-\> Change Directory…* from the drop-down menu and select the location
you want to act as the directory. These steps must be taken every time R
is restarted, otherwise it will be reset to R’s default (usually ‘My
Documents’). This can be done using the `setwd` function:

``` r
setwd("C://My Documents/Training")
```

Sets the working directory to the ‘Training’ folder in ‘My Documents’.

``` r
get(wd)
```

Returns the current working directory

``` r
list.files( )
```

Returns a list of all the files that currently exist within your working
directory. This is particularly useful when loading datasets from the
directory into R as they can be copy and pasted into the script to avoid
spelling mistakes and error messages.

#### 6.2.1 RStudio projects

Although working directories can be set manually using the `setwd`
command, this requires an absolute file path which makes it liable to
break easily (for example, if the folder is moved to a different
location) and makes it difficult to share code with others. An
alternative approach is to use RStudio projects which keeps all
associated files, including data, script files and outputs, grouped
together. Rather than requiring an absolute file path, *projects* (files
with the extension *.Rproj*) set the working directory relative to their
location.

To create a new project, choose *File -\> New project…* from the
drop-down menu. The project can either be created in a brand-new
directory, where a working directory does not already exist, or within
an existing directory. Existing projects can be opened by selecting
*File -\> Open project…* from the drop-down menu.

RStudio projects help create an efficient workflow by grouping all files
necessary for each analysis project together and assists collaboration
by setting a working directory relative to the .Rproj files’ location.

### 6.3 Data input

The easiest way to upload data from excel is to convert it into a
comma-delimited file (*.csv*). R has functions that can easily read and
convert csv files into objects within the R environment. Before
converting files, it is essential to check that they are correctly
formatted. Excel files should only contain one sheet of data with no
pictures or graphics, each row should correspond to a case or
observation and each column should correspond to a variable.

Once the spreadsheet has been converted into a .csv file, it can be read
into R using the `read_csv` function. For example, the following code
reads in the core spending power report from 2020 from *data* folder of
the current working directory and saves it as an object named
`csp_2020`:

``` r
csp_2020 <- read_csv("data/CSP_2020.csv")
```

    ## Rows: 396 Columns: 9
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (3): ons_code, authority, region
    ## dbl (6): sfa_2020, under_index_2020, ct_total_2020, nhb_2020, nhb_return_202...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

If the file is saved somewhere other than the current working directory,
the file path would need to be included in the brackets.

This function assumes that the first row of the .csv file contains
variable names. If that is not the case, the argument
`col_names = FALSE` must be added after a comma in the function.

For full details of the default arguments used in `read_csv`, search for
the help file using the `?read_csv` command.

Imported datasets will appear in the Environment window of the console
once they are saved as objects. This window shows the number of
variables and observations in each object. To view the contents of an
object, click on its name in the Environment window or use the function
`View(data)`. Useful functions that help explore a dataset include:

``` r
names(csp_2020)
```

    ## [1] "ons_code"         "authority"        "region"           "sfa_2020"        
    ## [5] "under_index_2020" "ct_total_2020"    "nhb_2020"         "nhb_return_2020" 
    ## [9] "rsdg_2020"

Returns a list of variable names

``` r
str(csp_2020)
```

    ## spc_tbl_ [396 × 9] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ ons_code        : chr [1:396] "E07000223" "E07000026" "E07000032" "E07000224" ...
    ##  $ authority       : chr [1:396] "Adur" "Allerdale" "Amber Valley" "Arun" ...
    ##  $ region          : chr [1:396] "SE" "NW" "EM" "SE" ...
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
    ##   ..   sfa_2020 = col_double(),
    ##   ..   under_index_2020 = col_double(),
    ##   ..   ct_total_2020 = col_double(),
    ##   ..   nhb_2020 = col_double(),
    ##   ..   nhb_return_2020 = col_double(),
    ##   ..   rsdg_2020 = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

Displays information about the structure of an object. This differs
depending on the type of object entered. For example, this object is a
tibble (Tidyverse’s name for a dataset). The information given about
tibbles includes the object dimensions (396 x 9, or 396 rows and 9
columns), variable names, and variable types.

``` r
head(csp_2020)
```

    ## # A tibble: 6 × 9
    ##   ons_code  authority    region sfa_2020 under_index_2020 ct_total_2020 nhb_2020
    ##   <chr>     <chr>        <chr>     <dbl>            <dbl>         <dbl>    <dbl>
    ## 1 E07000223 Adur         SE         1.77           0.0708          6.53   0.0881
    ## 2 E07000026 Allerdale    NW         3.85           0.147           5.40   0.606 
    ## 3 E07000032 Amber Valley EM         3.23           0.129           6.85   1.58  
    ## 4 E07000224 Arun         SE         3.67           0.147          11.6    2.29  
    ## 5 E07000170 Ashfield     EM         4.08           0.156           6.42   1.15  
    ## 6 E07000105 Ashford      SE         2.88           0.115           7.92   3.05  
    ## # ℹ 2 more variables: nhb_return_2020 <dbl>, rsdg_2020 <dbl>

Returns the first 6 rows of the tibble.

``` r
tail(csp_2020)
```

    ## # A tibble: 6 × 9
    ##   ons_code  authority   region sfa_2020 under_index_2020 ct_total_2020 nhb_2020
    ##   <chr>     <chr>       <chr>     <dbl>            <dbl>         <dbl>    <dbl>
    ## 1 E07000229 Worthing    SE         2.69            0.108          9.52    0.961
    ## 2 E07000238 Wychavon    WM         2.65            0.106          6.29    4.73 
    ## 3 E07000007 Wycombe     SE         0               0              0       0    
    ## 4 E07000128 Wyre        NW         3.41            0.137          7.64    1.28 
    ## 5 E07000239 Wyre Forest WM         2.84            0.114          7.45    0.262
    ## 6 E06000014 York        YH        27.1             1.06          93.8     2.68 
    ## # ℹ 2 more variables: nhb_return_2020 <dbl>, rsdg_2020 <dbl>

Returns the final 5 rows of the tibble.

### 6.4 Selecting variables

There are a number of ways to select individual variables within a
dataset within base R or tidyverse.

To select one or more variables using tidyverse, we can use the `select`
function:

`select(data, variable1, variable2, ...)`

For example, if we wanted to return the new homes bonus (nhb) for each
local authority, the seventh column of the dataset, we can either select
this based on the variable name or its location in the object:

``` r
select(csp_2020, nhb_2020)
```

    ## # A tibble: 396 × 1
    ##    nhb_2020
    ##       <dbl>
    ##  1   0.0881
    ##  2   0.606 
    ##  3   1.58  
    ##  4   2.29  
    ##  5   1.15  
    ##  6   3.05  
    ##  7   0     
    ##  8   0     
    ##  9   1.05  
    ## 10   1.85  
    ## # ℹ 386 more rows

``` r
select(csp_2020, 7)
```

    ## # A tibble: 396 × 1
    ##    nhb_2020
    ##       <dbl>
    ##  1   0.0881
    ##  2   0.606 
    ##  3   1.58  
    ##  4   2.29  
    ##  5   1.15  
    ##  6   3.05  
    ##  7   0     
    ##  8   0     
    ##  9   1.05  
    ## 10   1.85  
    ## # ℹ 386 more rows

We can select multiple variables and return them as a tibble by
separating the variable names or numbers with commas:

``` r
select(csp_2020, ons_code, authority, region)
```

    ## # A tibble: 396 × 3
    ##    ons_code  authority            region
    ##    <chr>     <chr>                <chr> 
    ##  1 E07000223 Adur                 SE    
    ##  2 E07000026 Allerdale            NW    
    ##  3 E07000032 Amber Valley         EM    
    ##  4 E07000224 Arun                 SE    
    ##  5 E07000170 Ashfield             EM    
    ##  6 E07000105 Ashford              SE    
    ##  7 E31000001 Avon Fire            SW    
    ##  8 E07000004 Aylesbury Vale       SE    
    ##  9 E07000200 Babergh              EE    
    ## 10 E09000002 Barking And Dagenham L     
    ## # ℹ 386 more rows

When selecting consecutive variables, a shortcut can be used that gives
the first and last variable in the list, separated by a colon, `:`. The
previous example can be carried out using the following code:

``` r
select(csp_2020, ons_code:region)
```

    ## # A tibble: 396 × 3
    ##    ons_code  authority            region
    ##    <chr>     <chr>                <chr> 
    ##  1 E07000223 Adur                 SE    
    ##  2 E07000026 Allerdale            NW    
    ##  3 E07000032 Amber Valley         EM    
    ##  4 E07000224 Arun                 SE    
    ##  5 E07000170 Ashfield             EM    
    ##  6 E07000105 Ashford              SE    
    ##  7 E31000001 Avon Fire            SW    
    ##  8 E07000004 Aylesbury Vale       SE    
    ##  9 E07000200 Babergh              EE    
    ## 10 E09000002 Barking And Dagenham L     
    ## # ℹ 386 more rows

The `select` function can be combined with a number of other ‘helper’
functions that allow us to select variables with certain characteristics
or naming conventions. For example:

`starts_with("xyz")` returns all variables where the name begins “xyz”.

`ends_with("xyz")` returns all variables where the name ends “xyz”.

`everything()` returns all variables.

For a full list of selection helpers, checkthe help file
`?tidyr_tidy_select`.

The `select` function returns the variable(s) in the form of a tibble
(or dataset). However, some functions, such as basic summary functions,
require data to be entered as a vector (a list of values). Tibbles with
a single variable can be converted into a vector using the `as.vector`
function, or we can use the base R approach to selecting a single
variable which returns the data as a vector by default:

``` r
csp_2020$nhb_2020
```

It is important to save any changes made to the existing dataset. This
can be done using the `write_csv` function:

``` r
write_csv(csp_2020, file = "data/csp_2020_new.csv")
```

When saving updated data, be sure to give it a different name to the raw
data file, otherwise the original data will be overwritten. It is
important to keep a copy of the raw data.

### 6.5 Filtering data

Filtering data allows us to select subgroups based on conditional
statements. If the observation meets the conditional statement, it will
be returned. The `filter` function from the Tidyverse package `dplyr`
can be used to return these subgroups:

`filter(data, condition 1, condition 2, ...)`

Conditional statements include less than `<`, less than or equal to
`<=`, greater than `>`, greater or equal to `>=`, is equal to `==`, is
not equal to `!=`, or is missing `is.na(variable)`.

For example, to return the core spending power for local authorities in
the North West region:

``` r
filter(csp_2020, region == "NW")
```

    ## # A tibble: 46 × 9
    ##    ons_code  authority   region sfa_2020 under_index_2020 ct_total_2020 nhb_2020
    ##    <chr>     <chr>       <chr>     <dbl>            <dbl>         <dbl>    <dbl>
    ##  1 E07000026 Allerdale   NW         3.85            0.147          5.40   0.606 
    ##  2 E07000027 Barrow-in-… NW         4.40            0.125          4.74   0.0111
    ##  3 E06000008 Blackburn … NW        58.1             1.79          55.9    0.999 
    ##  4 E06000009 Blackpool   NW        63.3             1.94          60.1    0.266 
    ##  5 E08000001 Bolton      NW        84.2             2.73         115.     0.506 
    ##  6 E07000117 Burnley     NW         5.90            0.171          7.16   0.694 
    ##  7 E08000002 Bury        NW        42.3             1.44          89.0    0.458 
    ##  8 E07000028 Carlisle    NW         3.34            0.134          7.49   1.49  
    ##  9 E06000049 Cheshire E… NW        42.5             1.70         230.    11.2   
    ## 10 E31000006 Cheshire F… NW        13.5             0.380         30.1    0     
    ## # ℹ 36 more rows
    ## # ℹ 2 more variables: nhb_return_2020 <dbl>, rsdg_2020 <dbl>

We can use multiple conditional statements to filter a subgroup, these
statements must be separated in the function using commas. For example,
to return a subgroup of local authorities that were in the North West
region and had a settlement funding assessment (SFA) of over £40
million, we use the following:

``` r
filter(csp_2020, region == "NW", sfa_2020 > 40)
```

    ## # A tibble: 23 × 9
    ##    ons_code  authority   region sfa_2020 under_index_2020 ct_total_2020 nhb_2020
    ##    <chr>     <chr>       <chr>     <dbl>            <dbl>         <dbl>    <dbl>
    ##  1 E06000008 Blackburn … NW         58.1             1.79          55.9    0.999
    ##  2 E06000009 Blackpool   NW         63.3             1.94          60.1    0.266
    ##  3 E08000001 Bolton      NW         84.2             2.73         115.     0.506
    ##  4 E08000002 Bury        NW         42.3             1.44          89.0    0.458
    ##  5 E06000049 Cheshire E… NW         42.5             1.70         230.    11.2  
    ##  6 E06000050 Cheshire W… NW         56.3             2.12         196.    10.2  
    ##  7 E10000006 Cumbria     NW        107.              3.56         248.     0.824
    ##  8 E47000001 Greater Ma… NW         50.6             1.28          50.5    0    
    ##  9 E06000006 Halton      NW         45.6             1.45          52.2    2.21 
    ## 10 E08000011 Knowsley    NW         84.1             2.50          56.8    2.10 
    ## # ℹ 13 more rows
    ## # ℹ 2 more variables: nhb_return_2020 <dbl>, rsdg_2020 <dbl>

### 6.6 Pipes

The `filter` and `select` functions can be combined to create an
analysis dataset that just contains data we need for our current
problem. Rather than carrying out these functions separately and
creating multiple objects, we can use a ‘pipe’. A pipe is represented be
the `%>%` symbol and can be read as ‘and then’ within code. Pipes allow
us to carry out multiple steps in the same process whilst ensuring the
code is still readable. For example, we can return a list of local
authority names from the North West region:

``` r
csp_2020 %>% 
  filter(region == "NW") %>% 
  select(authority)
```

    ## # A tibble: 46 × 1
    ##    authority            
    ##    <chr>                
    ##  1 Allerdale            
    ##  2 Barrow-in-Furness    
    ##  3 Blackburn with Darwen
    ##  4 Blackpool            
    ##  5 Bolton               
    ##  6 Burnley              
    ##  7 Bury                 
    ##  8 Carlisle             
    ##  9 Cheshire East        
    ## 10 Cheshire Fire        
    ## # ℹ 36 more rows

The pipe can also be combined with the `filter` function to `count` the
number of observations that lie within a subgroup:

``` r
csp_2020 %>% 
  filter(region == "NW") %>% 
  count()
```

    ## # A tibble: 1 × 1
    ##       n
    ##   <int>
    ## 1    46

### 6.7 Adding new variables

In Tidyverse, the function `mutate` allows us to add new variables,
either by manually specifying them or by creating them from existing
variables. Multiple variables can be created within the same function
and are separated by a comma. For example, we can create a new variables
with the squared settlement funding assessment, and another that recodes
the council tax variable into a categorical variable with three levels
(low: below £5 million, medium: between £5 million and £15 million, and
high: above £15 million):

``` r
csp_2020_new <- csp_2020 %>% 
  mutate(sfa_2020_sq = sfa_2020 ^ 2,
         ct_2020_cat = cut(ct_total_2020, breaks = c(0, 5, 15, Inf),
                           labels = c("Low", "Medium", "High"),
                           include_lowest = TRUE))
```

## Exercise 3

1.  How many local authorities were included in the London region?

2.  Give three ways that it would be possible to select all spend
    variables (sfa_2020, nhb_2020, etc.) from the CSP_2020 dataset.

3.  Create a new tibble, `em_2020`, that just includes local authorities
    from the East Midlands.

- How many local authorities in the East Midlands had an SFA of between
  £5 and 10 million? (**Hint**: check the `filter` help file for a
  useful helper)
- Create a new variable with the total overall spend in 2020 for local
  authorities in the East Midlands.
