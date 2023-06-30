---
title: "R"
---

{{< hint warning >}}
I have not used R for a long time. Proceed at your own risk.
{{< /hint >}}

References:

- \(Private repo\) [loikein/my-jupyter-notes](https://github.com/loikein/my-jupyter-notes/tree/master/datacamp--data-science)

## Configuration

Set language on macOS: \([credit](https://stat.ethz.ch/R-manual/R-devel/library/base/html/EnvVar.html)\)

```shell
# (In .zshrc)

export LANG=en_US.UTF-8
```

Check all environment variables:

```r
Sys.getenv()

Sys.getlocale()
```

Check the location of `RHOME`:

```shell
R RHOME
```

## List of common packages

Install:

```r
## plot
install.packages("gapminder")
install.packages("dplyr")
install.packages("ggplot2")

## import
install.packages("readr")
install.packages("data.table")
install.packages("readxl")
install.packages("gdata")
install.packages("DBI")
install.packages("httr")
install.packages("jsonlite")
install.packages("haven")
install.packages("foreign")

## clean
install.packages("tidyr")
install.packages("lubridate")
install.packages("stringr")

## function
install.packages("purrr")
```

Load:

```r
## plot
library(gapminder)
library(ggplot2)

## import
library(readr)
library(data.table)
library(readxl)
library(gdata)
library(DBI)
library(httr)
library(jsonlite)
library(haven)
library(foreign)

## data
library(dplyr)
library(hflights)

## clean
library(tidyr)
library(lubridate)
library(stringr)

## function
library(purrr)

## trading models
library(quantmod)
```

## Package: `base`

### `c()`

Append: \([credit](https://stackoverflow.com/a/22235924/10668706)\)

```r
vector <- c()
values <- c('a','b','c','d','e','f','g')

for (v in values){
  vector <- c(vector, v)
}
```

## Package: `distr`

Make distribution: \([credit](https://cran.r-project.org/web/packages/distr/vignettes/newDistributions-knitr.pdf)\)

```r
mean <- 1
sigma <- 0.25

(n <- Norm(mean=mean,sd=sigma))

# Distribution Object of Class: Norm
#  mean: 1
#  sd: 0.25
```

## Binder

{{< hint danger >}}
I have stopped using Binder. Proceed at your own risk.
{{< /hint >}}

Refs:

- [matthewfeickert/R-in-Jupyter-with-Binder: Example of how to use R in Jupyter notebooks and make compatible with Binder](https://github.com/matthewfeickert/R-in-Jupyter-with-Binder)
- [Configuration Files — Binder 0.1b documentation](https://mybinder.readthedocs.io/en/latest/using/config_files.html)

`runtime.txt`:

```text
r-2018-11-16
```

`requirements.txt`:

```text
jupyter_contrib_nbextensions
```

`postBuild`:

```sh
jupyter contrib nbextension install --user
jupyter nbextension enable toc2
jupyter trust binder-r-test.ipynb
```
