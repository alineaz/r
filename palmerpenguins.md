Palmer penguins dataset and ggplot2
================
Aline Azevedo Rocha
12/13/2021

### Introduction

This document was created to document my hands-on activity learning R.
This is an simple R Markdown document to demonstrate the use of the R
language with the Palmer Penguins dataset. The data were collected and
made available by Dr. Kristen Gorman and the Palmer Station, Antarctica
LTER, a member of the Long Term Ecological Research Network and contains
measurements of 3 penguin species.

#### Step 1 - Installing the required packages for this demo:

    ## Installing package into '/cloud/lib/x86_64-pc-linux-gnu-library/4.1'
    ## (as 'lib' is unspecified)
    ## Installing package into '/cloud/lib/x86_64-pc-linux-gnu-library/4.1'
    ## (as 'lib' is unspecified)

    ## also installing the dependencies 'colorspace', 'sys', 'bit', 'ps', 'rappdirs', 'rematch', 'farver', 'labeling', 'munsell', 'RColorBrewer', 'viridisLite', 'askpass', 'bit64', 'prettyunits', 'processx', 'backports', 'ellipsis', 'generics', 'assertthat', 'blob', 'DBI', 'lifecycle', 'R6', 'tidyselect', 'vctrs', 'withr', 'data.table', 'gargle', 'uuid', 'cellranger', 'curl', 'ids', 'rematch2', 'gtable', 'isoband', 'scales', 'cpp11', 'pkgconfig', 'openssl', 'fansi', 'utf8', 'clipr', 'vroom', 'tzdb', 'Rcpp', 'progress', 'callr', 'fs', 'selectr', 'broom', 'cli', 'crayon', 'dbplyr', 'dplyr', 'dtplyr', 'forcats', 'googledrive', 'googlesheets4', 'ggplot2', 'haven', 'hms', 'httr', 'lubridate', 'modelr', 'pillar', 'purrr', 'readr', 'readxl', 'reprex', 'rstudioapi', 'rvest', 'tibble', 'tidyr', 'xml2'

    ## Installing package into '/cloud/lib/x86_64-pc-linux-gnu-library/4.1'
    ## (as 'lib' is unspecified)
    ## Installing package into '/cloud/lib/x86_64-pc-linux-gnu-library/4.1'
    ## (as 'lib' is unspecified)

#### Step 2 - Loading the installed packages:

``` r
library("palmerpenguins")
library("tidyverse")
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.6     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
    ## ✓ readr   2.1.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library("dplyr")
library("ggplot2")
```

#### Step 3 - Loading the dataset:

``` r
data(package = 'palmerpenguins')
```

#### Step 4 - Getting to know the dataset with some basics commands

Checking the structure of palmerpenguins dataset:

``` r
str(penguins)
```

    ## tibble [344 × 8] (S3: tbl_df/tbl/data.frame)
    ##  $ species          : Factor w/ 3 levels "Adelie","Chinstrap",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ island           : Factor w/ 3 levels "Biscoe","Dream",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ bill_length_mm   : num [1:344] 39.1 39.5 40.3 NA 36.7 39.3 38.9 39.2 34.1 42 ...
    ##  $ bill_depth_mm    : num [1:344] 18.7 17.4 18 NA 19.3 20.6 17.8 19.6 18.1 20.2 ...
    ##  $ flipper_length_mm: int [1:344] 181 186 195 NA 193 190 181 195 193 190 ...
    ##  $ body_mass_g      : int [1:344] 3750 3800 3250 NA 3450 3650 3625 4675 3475 4250 ...
    ##  $ sex              : Factor w/ 2 levels "female","male": 2 1 1 NA 1 2 1 2 NA NA ...
    ##  $ year             : int [1:344] 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 ...

Checking the column names of the palmperpenguins dataset:

``` r
colnames(penguins)
```

    ## [1] "species"           "island"            "bill_length_mm"   
    ## [4] "bill_depth_mm"     "flipper_length_mm" "body_mass_g"      
    ## [7] "sex"               "year"

Data preview of palmerpenguins dataset:

``` r
head(penguins)
```

    ## # A tibble: 6 × 8
    ##   species island bill_length_mm bill_depth_mm flipper_length_… body_mass_g sex  
    ##   <fct>   <fct>           <dbl>         <dbl>            <int>       <int> <fct>
    ## 1 Adelie  Torge…           39.1          18.7              181        3750 male 
    ## 2 Adelie  Torge…           39.5          17.4              186        3800 fema…
    ## 3 Adelie  Torge…           40.3          18                195        3250 fema…
    ## 4 Adelie  Torge…           NA            NA                 NA          NA <NA> 
    ## 5 Adelie  Torge…           36.7          19.3              193        3450 fema…
    ## 6 Adelie  Torge…           39.3          20.6              190        3650 male 
    ## # … with 1 more variable: year <int>

### Using ggplot2 package to create data viz based on penguins measurements

Here I am using the ggplot2 package to create a scatter plot to
visualize the correlation of the flipper size of the penguins
(flipper_size_mm) with its body mass (body_mass_g).

#### Step 1:

The following is happening in the code chunk below:

Using geom_point to create a scatter plot; Using mapping to specify the
aesthetic (aes) based on x and y; Using flipper_length_mm and
body_mass_g as the axis to check the correction of these two values;
Adding a title and label descriptions:

``` r
ggplot(data=penguins) + 
geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g)) +
labs(title="Palmer Penguins", x = "Penguin's flipper lenght", y = "Penguin's size")
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](palmerpenguins_files/figure-gfm/step%201-1.png)<!-- -->

#### Step 2:

Adding color to distinct the color of each point based on the species
value for the penguins:

``` r
ggplot(data=penguins) + 
geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g,color=species)) +
labs(title="Palmer Penguins", x = "Penguin's flipper lenght", y = "Penguin's size")
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](palmerpenguins_files/figure-gfm/adding%20color-1.png)<!-- -->

#### Step 3:

Using shape to distinct the shape of each point based on the species
value for the penguins:

``` r
ggplot(data=penguins) + 
geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g,color=species,shape=species)) +
labs(title="Palmer Penguins", x = "Penguin's flipper lenght", y = "Penguin's size")
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](palmerpenguins_files/figure-gfm/adding%20shape-1.png)<!-- -->

#### Step 4:

Adding another layer to the plot, using geom_smooth to create a visible
trend line based in the same axis:

``` r
ggplot(data=penguins) + 
geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g,color=species,shape=species)) +
labs(title="Palmer Penguins", x = "Penguin's flipper lenght", y = "Penguin's size") +
geom_smooth(mapping = aes(x=flipper_length_mm, y=body_mass_g))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

    ## Warning: Removed 2 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](palmerpenguins_files/figure-gfm/adding%20another%20layer-1.png)<!-- -->

#### Step 5:

Adding another layer to the plot, facet wrap to create one plot for each
penguin species:

``` r
ggplot(data=penguins) + 
geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g,color=species,shape=species)) +
labs(title="Palmer Penguins", x = "Penguin's flipper lenght", y = "Penguin's size") +
geom_smooth(mapping = aes(x=flipper_length_mm, y=body_mass_g)) +
facet_wrap(~species)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

    ## Warning: Removed 2 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](palmerpenguins_files/figure-gfm/adding%20more%20layers-1.png)<!-- -->

### Learning conclusions:

With this simple document, we can conclude that the bigger the penguin,
the longer the flipper. :)

It seems an obvious conclusion, but this document was created to show
that data viz can be really useful to check correlations and tendencies
when analyzing data. Also, demonstrated the use of R Markdown and the
ggplot2 package.
