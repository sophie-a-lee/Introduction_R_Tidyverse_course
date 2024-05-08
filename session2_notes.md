Introduction to R with Tidyverse
================
Sophie Lee
2024-05-08

- <a href="#chapter-5-r-packages-and-add-ons"
  id="toc-chapter-5-r-packages-and-add-ons">Chapter 5: R packages and
  add-ons</a>
- <a href="#chapter-6-opening-and-exploring-data"
  id="toc-chapter-6-opening-and-exploring-data">Chapter 6: Opening and
  exploring data</a>
  - <a href="#61-tidyverse" id="toc-61-tidyverse">6.1 Tidyverse</a>
  - <a href="#62-the-working-directory"
    id="toc-62-the-working-directory">6.2 The working directory</a>

## Chapter 5: R packages and add-ons

R packages are a collection of functions and datasets developed by R
users that expand existing base R capabilities or add completely new
ones. Packages allow users to apply the most up-to-date methods shortly
after they are developed unlike other statistical software packages that
require an entirely new version. The quickest way to install a package
in R is:

`install.packages(‘name of package’)`

Once a package has been installed, use the following code to load it
into your R session:

`require(name of package)`

or

`library(name of package)`

R requires an internet connection to install a package. After
installation, packages must be loaded every time R is opened. It is good
practice to include the require or library command at the beginning of a
script file. All available packages listed on the [R
website](https://cran.r-project.org/web/packages/available_packages_by_name.html)
with details of what each one does. Use the `installed.packages( )` for
a list of all installed packages on your machine.

## Chapter 6: Opening and exploring data

### 6.1 Tidyverse

Up to this point in the course, we have been using a style of R coding
language (or syntax) known as base R, the original version of the
language and one that does not require any additional packages. However,
there are different approaches that have been developed within R
packages. For example, the Tidyverse set of packages, which aim to
improve certain aspects of R syntax.

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

    ## Warning: package 'tidyverse' was built under R version 4.2.3

    ## Warning: package 'tibble' was built under R version 4.2.3

    ## Warning: package 'readr' was built under R version 4.2.3

    ## Warning: package 'dplyr' was built under R version 4.2.3

    ## Warning: package 'lubridate' was built under R version 4.2.3

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
alternative approach is the use of RStudio projects which keeps all
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
