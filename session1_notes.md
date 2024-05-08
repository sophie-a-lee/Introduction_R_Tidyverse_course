Introduction to R with Tidyverse
================
Sophie Lee
2024-05-08

- <a href="#chapter-1-introduction-to-rstudio"
  id="toc-chapter-1-introduction-to-rstudio">Chapter 1: Introduction to
  RStudio</a>
  - <a href="#11-rstudio-console-window"
    id="toc-11-rstudio-console-window">1.1 RStudio console window</a>
  - <a href="#exercise-1" id="toc-exercise-1">Exercise 1</a>
- <a href="#chapter-2-introduction-to-r-programming"
  id="toc-chapter-2-introduction-to-r-programming">Chapter 2: Introduction
  to R programming</a>
  - <a href="#exercise-2" id="toc-exercise-2">Exercise 2</a>
- <a href="#chapter-3-r-objects-and-functions"
  id="toc-chapter-3-r-objects-and-functions">Chapter 3: R objects and
  functions</a>
- <a href="#chapter-4-help-and-error-messages"
  id="toc-chapter-4-help-and-error-messages">Chapter 4: Help and error
  messages</a>

## Chapter 1: Introduction to RStudio

There are a number of software packages based on the R programming
language aimed at making writing and running analyses easier for users.
They all run R in the background but look different and contain
different features. RStudio has been chosen for this course as it allows
users to create script files, allowing code to be re-run, edited, and
shared easily; RStudio also provides tools to help easily identify
errors in R code, integrates help documentation into the main console
and uses colour-coding to help read code at a glance.

RStudio is free to download for Windows, Mac or Linux from the following
website:

<https://posit.co/>

The basic R software must be installed before Rstudio can be used, this
can be downloaded from:

<https://cran.r-project.org/>

### 1.1 RStudio console window

The screenshot below shows the RStudio interface which comprises of four
windows: the R script file (A), the console (B), environment and history
(C), and files, packages and help (D).

![RStudio interface](images/rstudio_ide.png)

**Window A: R script files**

All analysis and actions in R are carried out using the R syntax
language. R script files allow you to write and edit code before running
it in the console window. If this window is not visible, create a new
script file using *File -\> New File -\> R Script* from the drop-down
menus or clicking the ![](images/new_file_shortcut.png) symbol above the
console and selecting *R Script*. This will open a new, blank script
file. More than one script file can be open at the same time.

Code entered into the script file does not run automatically. To run
commands from the script, highlight the code and click
![](images/run_shortcut.png) (this can be carried out by pressing
*Ctrl + Enter* in Windows or *Cmnd + Enter* on a Mac computer). More
than one command can be run at the same time by highlighting all of
them.

The main advantage of using the script file rather than entering the
code directly into the console is that it can be saved, edited and
shared for future reference. To save a script file, select *File -\>
Save As…* from the drop down menu or use the ![](images/save.png) icon
at the top of the window. It is important to save the script files at
regular intervals to avoid losing work. Past script files can be opened
using *File -\> Open File…* from the drop-down menu or by clicking the
![](images/open_shortcut.png) icon and selecting a .R file.

**Window B: The R console**

This is where all commands run from the script file, results other than
graphics, and error messages are displayed. Commands can be written
directly into the R console after the `>` symbol and executed using the
Enter key. It is not recommended to write code directly into the console
as it is cannot be saved and replicated.

To clear the text from the console, leaving a blank white screen, press
*Ctrl + L* for Windows and *Cmnd + L* on Mac computers. This command
will only clear the text and will not remove any saved objects.

**Window C: Environment and history**

This window lists all data and objects currently loaded into R. More
details on the types of objects and how to use the Environment window
are given in later sections.

**Window D: Files, plots, packages and help**

This window has many potential uses: graphics are displayed and can be
saved from here, and R help files will appear here. This window is only
available in the RStudio interface and not in the basic R package.

### Exercise 1

1.  Open a new script file if you have not already done so.

2.  Save this script file into an appropriate location using Save as…
    from the drop-down menu

## Chapter 2: Introduction to R programming

All analyses within R is carried out using *syntax*, the R programming
language. It is important to note that R is case-sensitive so always
ensure that you use the correct combination of upper and lower case
letters when running functions or calling objects. Any text written in
the R console or script file can be treated the same as text from other
documents or programmes: text can be highlighted, copied and pasted as
in Word documents to make coding more efficient. When creating script
files, it is important to ensure they are clear and easy to read.
Comments can be added to script files using the `#` symbol. R will
ignore any text following this symbol on the same line.

The choice of brackets in R coding is particularly important as they all
have different functions. Round brackets `( )` are the most commonly
used as they define arguments of functions. Any text followed by round
brackets is assumed to be a function and R will attempt to run it.
Square brackets `[ ]` are used to set criteria or conditions within a
function or object. Curly brackets `{ }` are used within loops, when
creating a new function, and within `for` and `if` functions. If the
name of a function is not followed by round brackets, R will return the
algorithm for the function within the console.

All standard notation for mathematical calculations (`+, -, *, /, ^`,
etc.) are compatible with R. At its simplest level, R is a powerful
calculator.

### Exercise 2

1.  Add your name and the date to the top of your script file (hint:
    comment this out so R does not try to run it)

2.  Use R to answer to following and write the answers within the script
    file:

- $64^2$
- $12687 - 85221$
- $3432 \div 8$
- $96 \times 72$

## Chapter 3: R objects and functions

One of the main advantages to using R over other software packages such
as SPSS is that more than one dataset can be accessed at the same time.
A collection of data stored in any format within R is known as an
**object**. Objects can be single numbers, single variables, entire
datasets or lists of datasets.

Objects are defined in R using the `<-` symbol (the ‘less than’ symbol
followed by a dash. Note that there is no space between these as this
changes the meaning of the symbol to ‘less than, minus’) or `=`. For
example, by typing `obj1 <- 81` or `obj1 = 81`, an object called `obj1`
is defined with the value 81 and will appear in the environment window
of the console. Throughout this booklet, the symbol `<-` will be used to
avoid confusion between the definition of an object and the mathematical
meaning of `=`.

To retrieve a saved object, type its name into the script or console and
run it. For example, if we type `obj1` into the console, 81 will appear.
This object can then be called in functions and calculations.

``` r
obj1 <- 81

obj1
```

    ## [1] 81

``` r
obj1 * 2
```

    ## [1] 162

R has some mathematical objects stored by default such as pi that can be
used in calculations.

``` r
pi
```

    ## [1] 3.141593

The `[1]` that appears at the beginning of each output line indicates
that this is the first element in the object. If there were two lines
then the second line would start with the number of that element in
square brackets. For example, if we had an object with 6 elements and
when called the first line contained the first 5 elements, each line
would begin with `[1]` and `[6]` respectively.

**Functions** are built-in commands that allow R users to run analyses.
All functions require the definition of arguments within round brackets.
For example, if we wanted to find out the square root or an object, we
could use the built-in `sqrt` function or if we wanted to find the
median of a group of numbers, we could use the built-in `median`
function.

To remove objects from the RStudio environment, use the `rm(objectname)`
function. To remove every object from the environment, use the command
`rm(list = ls())`. **IMPORTANT NOTE**: be cautious when using these
commands as they permanently delete objects and cannot be undone. The
only way to reverse this is to re-run the code that originally created
the objects.

## Chapter 4: Help and error messages

Each function that exists within R has an associated help file. To
retrieve these help files, enter `?` followed by the function name into
the console window, e.g `?mean`. The help file will appear in RStudio
containing the following sections:

- Description: what the function is used for
- Usage: how the function is used
- Arguments: required and optional arguments entered into round brackets
  necessary for the function to work
- Details: relevant details about the function in question
- References
- See also: links to other relevant functions
- Examples: example code with applications of the function

An internet connection is not required to access this documentation
within RStudio but these help pages are also available on the R website.

If a function is not defined correctly or there is some mistake in
syntax that has been run in the console, R is usually good at
identifying errors and providing informative error messages that include
the location of the error. For example:

``` r
plot(x, y)
```

    ## Error in plot(x, y): object 'x' not found

The objects `x` and `y` have not been defined within R and so the
command cannot run.

``` r
Sqrt(obj1)
```

    ## Error in Sqrt(obj1): could not find function "Sqrt"

R is case sensitive so cannot find the function `Sqrt`.

`obj1 +`

When working within the R console, if a command is run before it is
finished or if all brackets are not closed, a `+` symbol will appear on
the next line rather than `>`. This means that R expects you to keep
writing. To overcome this issue, either finish the command on the next
line or press the *esc* button on your keyboard to start from scratch.

One of the benefits of using RStudio rather than the basic R package is
that it will suggest object or function names after typing the first few
letters. This avoids spelling mistakes and accidental errors when
running code. To accept the suggestion, either click the correct choice
with your mouse or use the *tab* button on your keyboard.