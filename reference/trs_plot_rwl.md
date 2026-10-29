# Plot all series in a tree-ring width dataframe

Creates a line plot of all tree-ring series in an rwl dataframe, with
optional z-score standardization and faceting options.

## Usage

``` r
trs_plot_rwl(
  x,
  zscore = TRUE,
  facet = FALSE,
  ncol = 1,
  color = NULL,
  scale_y = "fixed"
)
```

## Arguments

- x:

  A `data.frame` (typically of class `'rwl'`) with multiple columns of
  ring-width values. Row names must be numeric and represent calendar
  years.

- zscore:

  Logical. If `TRUE`, the ring-width series are standardized to z-scores
  before plotting. Defaults to `TRUE`.

- facet:

  Logical. If `TRUE`, creates a faceted plot with each series in a
  separate panel. If `FALSE`, plots all series overlaid on the same
  plot. Defaults to `FALSE`.

- ncol:

  Numeric. Number of columns for faceted plots (only used when
  `facet = TRUE`). Defaults to `1`.

- color:

  Character string or vector specifying line color(s). When `NULL` and
  `facet = FALSE`, each series gets a different color. When a single
  color is specified, all lines use that color. When a vector of colors
  is provided, each series gets the corresponding color. Defaults to
  `NULL`.

- scale_y:

  Character string specifying y-axis scaling for faceted plots. Options
  are "fixed", "free", "free_x", or "free_y". Defaults to `"fixed"`.

## Value

A `ggplot` object showing the plotted time series.

## Details

The function assumes that the rwl dataframe is already calendar-dated
with years as row names. When `facet = FALSE`, all series are plotted on
the same axes with different colors. When `facet = TRUE`, each series
gets its own panel for easier individual inspection. When providing a
vector of colors, the length must match the number of series in the
data. Required helper functions include:
[`trs_trim`](https://docs.ropensci.org/fellingdater/reference/trs_trim.md)
and
[`trs_zscore`](https://docs.ropensci.org/fellingdater/reference/trs_zscore.md).

Required packages: **ggplot2**, **plyr**, **tidyr**, **dplyr**

## Examples

``` r
rwl_data <- trs_pseudo_rwl(n_series = 5, series_length = c(75, 100), end_date = c(2000, 2025))

# Overlaid plot with z-scores
trs_plot_rwl(rwl_data, zscore = TRUE, facet = FALSE)
#> Error in `[[<-.data.frame`(`*tmp*`, col, value = c(1.19752876866083, 1.12428541889564, 0.611581970539321, 1.12428541889564, 0.904555369600073, -0.413824926173313, -0.0476081773473727, -0.633554975468878, -0.0476081773473727, 0.611581970539321, 0.172121871948192, -0.267338226642937, 0.0988785221830036, 0.538338620774132, -0.413824926173313, -0.853285024764442, -2.17166532053783, -2.31815202006821, -1.29274512335557, -1.29274512335557, -1.80544857171189, -1.58571852241632, -2.53788206936377, -1.65896187218151, -0.487068275938502, 0.538338620774132, 0.758068670069697, 0.465095271008944, -0.0476081773473727, 0.318608571478568, 0.831312019834885, -0.194094876877749, 0.0256351724178154, -0.56031162570369, -0.633554975468878, -0.853285024764442, -0.999771724294819, -1.36598847312076, -0.633554975468878, -0.633554975468878, -0.706798325234066, -0.706798325234066, -1.14625842382519, -0.780041674999254, 0.391851921243756, 0.24536522171338, -2.02517862100745, -1.58571852241632, -1.29274512335557, -0.853285024764442, 0.318608571478568, -0.0476081773473727, 0.684825320304509, 1.05104206913045, 1.41725881795639, 1.27077211842601, 0.538338620774132, 1.27077211842601, 1.12428541889564, 1.3440154681912, 1.3440154681912, 0.758068670069697, 1.3440154681912, 1.19752876866083, 0.611581970539321, 0.465095271008944, 1.27077211842601, 1.05104206913045, 0.24536522171338, 0.465095271008944, -0.267338226642937, 0.0988785221830036, 0.904555369600073, 0.684825320304509, 0.904555369600073, 0.538338620774132, 0.977798719365261, 0.538338620774132, 0.0256351724178154, 0.758068670069697)): replacement has 80 rows, data has 104

# Faceted plot with raw values
trs_plot_rwl(rwl_data, zscore = FALSE, facet = TRUE, ncol = 1)
#> Ignoring unknown labels:
#> • colour : ""


# Custom colors for each series
col_vec <- c("#0fa3b1", "#07beb8", "#3dccc7", "#68d8d6", "#9ceaef")
trs_plot_rwl(rwl_data, color = c("tomato3", "navyblue", "forestgreen", "purple", "orange"))
#> Error in `[[<-.data.frame`(`*tmp*`, col, value = c(1.19752876866083, 1.12428541889564, 0.611581970539321, 1.12428541889564, 0.904555369600073, -0.413824926173313, -0.0476081773473727, -0.633554975468878, -0.0476081773473727, 0.611581970539321, 0.172121871948192, -0.267338226642937, 0.0988785221830036, 0.538338620774132, -0.413824926173313, -0.853285024764442, -2.17166532053783, -2.31815202006821, -1.29274512335557, -1.29274512335557, -1.80544857171189, -1.58571852241632, -2.53788206936377, -1.65896187218151, -0.487068275938502, 0.538338620774132, 0.758068670069697, 0.465095271008944, -0.0476081773473727, 0.318608571478568, 0.831312019834885, -0.194094876877749, 0.0256351724178154, -0.56031162570369, -0.633554975468878, -0.853285024764442, -0.999771724294819, -1.36598847312076, -0.633554975468878, -0.633554975468878, -0.706798325234066, -0.706798325234066, -1.14625842382519, -0.780041674999254, 0.391851921243756, 0.24536522171338, -2.02517862100745, -1.58571852241632, -1.29274512335557, -0.853285024764442, 0.318608571478568, -0.0476081773473727, 0.684825320304509, 1.05104206913045, 1.41725881795639, 1.27077211842601, 0.538338620774132, 1.27077211842601, 1.12428541889564, 1.3440154681912, 1.3440154681912, 0.758068670069697, 1.3440154681912, 1.19752876866083, 0.611581970539321, 0.465095271008944, 1.27077211842601, 1.05104206913045, 0.24536522171338, 0.465095271008944, -0.267338226642937, 0.0988785221830036, 0.904555369600073, 0.684825320304509, 0.904555369600073, 0.538338620774132, 0.977798719365261, 0.538338620774132, 0.0256351724178154, 0.758068670069697)): replacement has 80 rows, data has 104
trs_plot_rwl(rwl_data, color = col_vec, zscore = FALSE)

```
