# R

## General

Set language on macOS: ([ref](https://stat.ethz.ch/R-manual/R-devel/library/base/html/EnvVar.html))

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
