---
weight: 750
title: "Regression"
---

## Regression with `statsmodels`

[statsmodels 0.14.0](https://www.statsmodels.org/stable/index.html)

> R-style formulas (e.g. `smf.ols`) do not need manually adding constant, while plain formulas (e.g. `sm.OLS`) need.
{.book-hint .warning}

### OLS

Doc: [statsmodels.regression.linear_model.OLSResults - statsmodels 0.14.0](https://www.statsmodels.org/stable/generated/statsmodels.regression.linear_model.OLSResults.html)

```python
import numpy as np
import statsmodels.api as sm
import statsmodels.formula.api as smf

# formula
formula_1 = "y ~ x1 + x2 + ..."

# fit
results = smf.ols(formula_1, data=df).fit()

# results: two types of tables
print(results.summary())
print(results.summary2())
```

If want to include all (but one) columns of df:

```python
formula_1 = "y ~ " + " + ".join(df.columns[1:])
```

If want hetroskedasticity-robust standard errors:

```python
results = smf.ols(formula_1, data=df).fit(cov_type="HC3")
```

Get results in tables: \([doc](https://www.statsmodels.org/stable/generated/statsmodels.iolib.table.SimpleTable.html)\)

```python
# statsmodels.iolib.table.SimpleTable
results.summary().tables[0]
results.summary().tables[1].as_html()
results.summary().tables[2].as_latex_tabular(center=False)
```

{{< details "List all attributes/methods of some object" >}}
Credit: [python - How to retrieve model estimates from statsmodels? - Stack Overflow](https://stackoverflow.com/a/48522820/10668706)\)

```python
for attr in dir(results):
    if not attr.startswith('_'):
        print(attr)
```
{{< /details >}}

### Make tables with `stargazer`

Doc \(?\): [mwburke/stargazer: Python implementation of the R stargazer multiple regression model creation tool](https://github.com/mwburke/stargazer)  
Main examples: [stargazer/examples.ipynb](https://github.com/mwburke/stargazer/blob/master/examples.ipynb)

```python
from stargazer.stargazer import Stargazer, LineLocation

stargazer = Stargazer([results]) # can have multiple specifications
# preview table
stargazer
# output latex code
print(stargazer.render_latex())
```

### Plots

Ref: [Predicting Housing Prices with Linear Regression using Python, pandas, and statsmodels – LearnDataSci](https://www.learndatasci.com/tutorials/predicting-housing-prices-linear-regression-using-python-pandas-statsmodels/)

## Regression with `sklearn`

TBE
