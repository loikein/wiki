---
title: "R"
---

# R

References:

- \(Private repo\) [loikein/my-jupyter-notes](https://github.com/loikein/my-jupyter-notes/tree/master/datacamp--data-science)

## Configuration

Set language on macOS: \([credit](https://stat.ethz.ch/R-manual/R-devel/library/base/html/EnvVar.html)\)

```text
# In .zshrc

export LANG=en_US.UTF-8
```

Check all environment variables:

```r
Sys.getenv()

Sys.getlocale()
```

Check the location of `RHOME`:

```bash
$ R RHOME
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
