Vignette
================

# Pokemon API

This vignette will show how to contact the Pokemon API () and how to use
the functions provided.

## Required packages

The following are the packages required to use the Pokemon API
functions.

``` r
install.packages(c("httr", "jsonlite"))
```

-   “httr” is used to help make the HTTP calls for the API
-   “jsonlite” is used to help parse the JSON data into an R list

## Getting Pokemon Character Information

The first method will be getting Pokemon character information. This
