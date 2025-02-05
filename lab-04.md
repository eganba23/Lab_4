Lab 04 - La Quinta is Spanish for next to Denny’s, Pt. 1
================
Benjamin Egan
2/5

### Exercise 1 - Look at Denny’s dataset

``` r
dennys %>%
  nrow()
```

    ## [1] 1643

``` r
dennys %>%
ncol()
```

    ## [1] 6

There are 1,643 rows and 6 columns in the Denny’s dataset

### Exercise 2 - Look at La Quinta dataset

``` r
laquinta %>%
  nrow()
```

    ## [1] 909

``` r
laquinta %>%
ncol()
```

    ## [1] 6

There are 909 rows and 6 columns in the La Quinta dataset

### Exercise 3 - International locations?

Based on the website, Denny’s is only based in the United States (if I
google it, apparently there are a handful of Denny’s located in Canada,
Mexico, etc.). For La Quinta, there are several hotels in China, New
Zealand, Turkey, the United Arab Emirates, Chile, Colombia, and
Ecquador. …

### Exercise 4 - Dataset observations

``` r
view(dennys)
view(laquinta)
```

Looking at the dataset, there is a column for states, latitude,
longitude. One way we could do this is by filtering out state
abbreviations. This should leave us with only international data.
Another way to do this is create a filter that filters out rows based on
their latitude and longitude. Any observations that match latitude and
longitude in the United states would be filtered out.

…

### Exercise 5 - Examine Denny’s dataset

``` r
dennys %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 0 × 6
    ## # ℹ 6 variables: address <chr>, city <chr>, state <chr>, zip <chr>,
    ## #   longitude <dbl>, latitude <dbl>

There are no Denny’s outside the United States in the dataset.

…

### Exercise 6 - USA Denny’s variable

``` r
dn <- dennys %>%
  mutate(country = "United States")
#view(dn)
```

…

### Exercise 7 - Examine La Quinta dataset

``` r
laquinta %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 14 × 6
    ##    address                                  city  state zip   longitude latitude
    ##    <chr>                                    <chr> <chr> <chr>     <dbl>    <dbl>
    ##  1 Carretera Panamericana Sur KM 12         "\nA… AG    20345    -102.     21.8 
    ##  2 Av. Tulum Mza. 14 S.M. 4 Lote 2          "\nC… QR    77500     -86.8    21.2 
    ##  3 Ejercito Nacional 8211                   "Col… CH    32528    -106.     31.7 
    ##  4 Blvd. Aeropuerto 4001                    "Par… NL    66600    -100.     25.8 
    ##  5 Carrera 38 # 26-13 Avenida las Palmas c… "\nM… ANT   0500…     -75.6     6.22
    ##  6 AV. PINO SUAREZ No. 1001                 "Col… NL    64000    -100.     25.7 
    ##  7 Av. Fidel Velazquez #3000 Col. Central   "\nM… NL    64190    -100.     25.7 
    ##  8 63 King Street East                      "\nO… ON    L1H1…     -78.9    43.9 
    ##  9 Calle Las Torres-1 Colonia Reforma       "\nP… VE    93210     -97.4    20.6 
    ## 10 Blvd. Audi N. 3 Ciudad Modelo            "\nS… PU    75010     -97.8    19.2 
    ## 11 Ave. Zeta del Cochero No 407             "Col… PU    72810     -98.2    19.0 
    ## 12 Av. Benito Juarez 1230 B (Carretera 57)… "\nS… SL    78399    -101.     22.1 
    ## 13 Blvd. Fuerza Armadas                     "con… FM    11101     -87.2    14.1 
    ## 14 8640 Alexandra Rd                        "\nR… BC    V6X1…    -123.     49.2

Places and state tags for international hotels: Mexico (AG) Mexico (QR)
Mexico (CH) Mexico (NL) Colombia (ANT) Mexico (NL) Mexico (NL) Canada
(ON) Mexico (VE) Mexico (PU) Mexico (PU) Mexico (SL) Honduras (FM)
Canada (BC)

…

### Exercise 8 - La Quinta Country Variable

``` r
lq_USA <- laquinta %>%
  mutate(country = case_when(
    state %in% state.abb ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    state == "ANT" ~ "Colombia",
    state %in% c("AG", "QR", "CH", "NL", "VE","PU","SL") ~ "Mexico",
    state == "FM" ~ "Honduras"
  ))

#view(lq)

lq <- lq_USA %>%
  filter(country == "United States")
```

…
