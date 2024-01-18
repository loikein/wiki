---
title: "R"
---

> I have not used R for a long time. Proceed at your own risk.
{.book-hint .warning}

Moved from: \(Private repo\) [loikein/my-jupyter-notes](https://github.com/loikein/my-jupyter-notes/tree/master/datacamp--data-science)

## \(Maybe\) Useful resources

- [Home | Bookdown](https://bookdown.org/)
- [An Introduction to Statistical Learning](https://www.statlearning.com/)
  + [Resources - ISL with R, 2nd Edition — An Introduction to Statistical Learning](https://www.statlearning.com/resources-second-edition)
- [cis-ds/course-site: Course site for Computing for Information Science (INFO 5940)](https://github.com/cis-ds/course-site)
- [swirldev/swirl_courses: :mortar_board: A collection of interactive courses for the swirl R package.](https://github.com/swirldev/swirl_courses#swirl-courses)
- [R for Data Science (1e)](https://r4ds.had.co.nz/index.html)
  + [R for Data Science (2e)](https://r4ds.hadley.nz/)
- [R Programming for Data Science](https://bookdown.org/rdpeng/rprogdatascience/)
- [The R Graph Gallery – Help and inspiration for R charts](https://r-graph-gallery.com/index.html)
- [R 语言教程 李东风](https://www.math.pku.edu.cn/teachers/lidf/docs/Rbook/html/_Rbook/index.html)
  + [A R软件基础(\*) | 统计计算 李东风](https://www.math.pku.edu.cn/teachers/lidf/docs/statcomp/html/_statcompbook/appendix-rintro.html)
- List: [XiangyunHuang/R-Tutorial: R 语言材料](https://github.com/XiangyunHuang/R-Tutorial)


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

> I have stopped using Binder. Proceed at your own risk.
{.book-hint .danger}

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
