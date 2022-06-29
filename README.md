Pokemon API Vignette
================

``` r
# Load packages
library(httr)
library(jsonlite)
library(tidyverse)
library(gridExtra)
library(ggplot2)
```

# Pokemon API

This vignette will show how to contact the Pokemon API
(<https://pokeapi.co/docs/v2>) and how to use the functions provided.

## Required packages

The following are the packages required to use the Pokemon API
functions.

``` r
install.packages(c("httr", "jsonlite", "tidyverse", "gridExtra"))
```

-   “httr” is used to help make the HTTP calls for the API
-   “jsonlite” is used to help parse the JSON data into an R list

## Getting Pokemon Character Information

The first method will be getting Pokemon character information. This
will give main attributes and stats on any Pokemon character. For
example, if we want stats from Pikachu we can call the following code:

``` r
ret <- get_pokemon_character("pikachu")
```

    ## Warning: `cols` is now required when using unnest().
    ## Please use `cols = c(stat)`

And can get information from the character from the return object, such
as the character’s stats.

``` r
ret$stats
```

    ## # A tibble: 6 × 4
    ##   base_stat effort name            url                              
    ##       <int>  <int> <chr>           <chr>                            
    ## 1        35      0 hp              https://pokeapi.co/api/v2/stat/1/
    ## 2        55      0 attack          https://pokeapi.co/api/v2/stat/2/
    ## 3        40      0 defense         https://pokeapi.co/api/v2/stat/3/
    ## 4        50      0 special-attack  https://pokeapi.co/api/v2/stat/4/
    ## 5        50      0 special-defense https://pokeapi.co/api/v2/stat/5/
    ## 6        90      2 speed           https://pokeapi.co/api/v2/stat/6/

### Exploratory Data Analysis

We can explore the data further by doing some analysis on it. For
instance, we may want to see a box plot of the base stat.

``` r
pikachu_stats <- ggplot(ret$stats, aes(x=base_stat)) +
  geom_boxplot()

pikachu_stats
```

![](/Users/jonathanwood/Documents/pokemonproject/README_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

And we can do this with multiple characters. Let’s also get the
character stats from Bulbasaur and compare his stats with Pikachu’s.

``` r
bulbasaur <- get_pokemon_character("bulbasaur")
```

    ## Warning: `cols` is now required when using unnest().
    ## Please use `cols = c(stat)`

``` r
bulbasaur
```

    ## $name
    ## [1] "bulbasaur"
    ## 
    ## $stats
    ## # A tibble: 6 × 4
    ##   base_stat effort name            url                              
    ##       <int>  <int> <chr>           <chr>                            
    ## 1        45      0 hp              https://pokeapi.co/api/v2/stat/1/
    ## 2        49      0 attack          https://pokeapi.co/api/v2/stat/2/
    ## 3        49      0 defense         https://pokeapi.co/api/v2/stat/3/
    ## 4        65      1 special-attack  https://pokeapi.co/api/v2/stat/4/
    ## 5        65      0 special-defense https://pokeapi.co/api/v2/stat/5/
    ## 6        45      0 speed           https://pokeapi.co/api/v2/stat/6/

``` r
bulbasaur_stats <- ggplot(bulbasaur$stats, aes(x=base_stat)) +
  geom_boxplot()

grid.arrange(pikachu_stats, bulbasaur_stats)
```

![](/Users/jonathanwood/Documents/pokemonproject/README_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->
