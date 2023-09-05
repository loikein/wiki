---
weight: 750
title: "Regression"
---

## Regression with `statsmodels`

[statsmodels 0.14.0](https://www.statsmodels.org/stable/index.html)

> R-style formulas (e.g. `smf.ols`) do not need manually adding constant, while plain formulas (e.g. `sm.OLS`) need.
{.book-hint .warning}

### OLS basics

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

### Formula

Use a lot of columns of df:

```python
formula = "y ~ " + " + ".join(df.columns[1:])
```

Interaction: \([ref](https://stackoverflow.com/a/35554431)\)

```python
# The followings are the same:
formula = "y ~ x1 * x2"
formula = "y ~ x1 + x2 + x1:x2"
```

### Standard error types

Doc: [statsmodels.regression.linear_model.RegressionResults.HC3_se - statsmodels 0.15.0](https://www.statsmodels.org/dev/generated/statsmodels.regression.linear_model.RegressionResults.HC3_se.html)

Get hetroskedasticity-robust standard errors:

```python
results = smf.ols(formula_1, data=df).fit(cov_type="HC3")
```

### Detect multicollinearity

Doc: [statsmodels.stats.outliers_influence.variance_inflation_factor - statsmodels 0.14.0](https://www.statsmodels.org/stable/generated/statsmodels.stats.outliers_influence.variance_inflation_factor.html)

Ref: [Detecting Multicollinearity with VIF - Python - GeeksforGeeks](https://www.geeksforgeeks.org/detecting-multicollinearity-with-vif-python/)

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

# make VIF dataframe
vif_data = pd.DataFrame()
vif_data["feature"] = df.columns

# calculating VIF for each feature
vif_data["VIF"] = [
    variance_inflation_factor(df.values, i) for i in range(len(df.columns))
]

print(vif_data)
```

### Get results in tables

Get results in tables: \([doc](https://www.statsmodels.org/stable/generated/statsmodels.iolib.table.SimpleTable.html)\)

```python
# statsmodels.iolib.table.SimpleTable
results.summary().tables[0]
results.summary().tables[1].as_html()
results.summary().tables[2].as_latex_tabular(center=False)
```

{{< details "List all attributes/methods of some object" >}}
Credit: [python - How to retrieve model estimates from statsmodels? - Stack Overflow](https://stackoverflow.com/a/48522820/10668706)

```python
for attr in dir(results):
    if not attr.startswith('_'):
        print(attr)
```
{{< /details >}}

### Get results programmatically

Refs:

- [python - How to extract the regression coefficient from statsmodels.api? - Stack Overflow](https://stackoverflow.com/a/47388554/10668706)
- [linear regression - How to get the P Value in a Variable from OLSResults in Python? - Stack Overflow](https://stackoverflow.com/questions/41075098/how-to-get-the-p-value-in-a-variable-from-olsresults-in-python)

```python
formula = "y ~ x1 + x2"
results = smf.ols(formula, data=df).fit()

coef = results.params["x1"]
p_val = results.pvalues["x1"]
```

### Loop of regressions

```python
results_list = []

for col in df.columns[1:]:
    # x1 is df.columns[0]
    formula = "y ~ x1" + " + " + str(col)
    results = smf.ols(formula, data=df).fit()
    
    corr = results.params[str(col)]
    p_val = results.pvalues[str(col)]

    dict = {"index": col, "corr": corr, "p_val": p_val}

    results_list.append(dict)

results_df = pd.DataFrame(results_list).set_index("index")
```

### Use with `stargazer`

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
