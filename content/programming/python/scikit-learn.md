---
weight: 800
title: "scikit-learn"
---
## Impute missing data

Doc: [6.4. Imputation of missing values — scikit-learn 1.3.0 documentation](https://scikit-learn.org/stable/modules/impute.html)

### `SimpleImputer`

```python
from sklearn.impute import SimpleImputer

# get # of rows with missing values
# ref: https://note.nkmk.me/en/python-pandas-nan-extract/
sum(df.isnull().any(axis=1))
# 230

# use imputer
imp_simple = SimpleImputer()
imp_simple.fit(df)

imp_simple_df = pd.DataFrame(
    data = imp_simple.transform(df),
    columns = list(df.columns),
    index = list(df.index),
)

# get # of rows with missing values
sum(imp_simple_df.isnull().any(axis=1))
# 0
```

### `IterativeImputer`

```python
from sklearn.experimental import enable_iterative_imputer   #noqa
from sklearn.impute import IterativeImputer

# get # of rows with missing values
sum(df.isnull().any(axis=1))
# 230

# use imputer
imp_iter = IterativeImputer(max_iter=10, random_state=0)
imp_iter.fit(df)

imp_iter_df = pd.DataFrame(
    data = imp_iter.transform(df),
    columns = list(df.columns),
    index = list(df.index),
)

# get # of rows with missing values
sum(imp_iter_df.isnull().any(axis=1))
# 0
```

## LASSO for variable selection

Docs:

- [sklearn.linear_model.Lasso — scikit-learn 1.3.0 documentation](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Lasso.html)
- [sklearn.linear_model.LassoCV — scikit-learn 1.3.0 documentation](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LassoCV.html#sklearn.linear_model.LassoCV)
- [1.1. Linear Models 1.1.3. Lasso — scikit-learn 1.3.0 documentation](https://scikit-learn.org/stable/modules/linear_model.html#lasso)
- [Lasso on dense and sparse data — scikit-learn 1.3.0 documentation](https://scikit-learn.org/stable/auto_examples/linear_model/plot_lasso_dense_vs_sparse_data.html)

Refs:

- [Lasso Regression with Python | Jan Kirenz](https://www.kirenz.com/post/2019-08-12-python-lasso-regression-auto/)
- [Lasso and Ridge Regression in Python Tutorial | DataCamp](https://www.datacamp.com/tutorial/tutorial-lasso-ridge-regression)
- [Common pitfalls in the interpretation of coefficients of linear models — scikit-learn 1.3.0 documentation](https://scikit-learn.org/stable/auto_examples/inspection/plot_linear_model_coefficient_interpretation.html)

### Normal Lasso

**Step 0**: All imports

```python
import numpy as np
import pandas as pd

from sklearn.model_selection import train_test_split
from sklearn.linear_model import Lasso, LassoCV
from sklearn.preprocessing import StandardScaler
```

**Step 1**: Split datasets

```python
# Assuming dependent variable is df.columns[0]
features = df.columns[1:]
target = df.columns[0]

# Get X and y values
X = df[features].values
y = df[target].values

# Split training set and testing set
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=10)
print("The dimension of X_train is", X_train.shape)
print("The dimension of X_test is", X_train.shape)
```

**Step 2**: Normalise the independent variables

```python
# scale features
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
```

**Step 3**: Run LASSO

```python
# Decide on some alpha
alpha = 0.001

# Lasso cross validation
lasso = Lasso(alpha=alpha, random_state=0).fit(X_train, y_train)

# Get R2 values
lasso_r2_train = lasso.score(X_train,y_train)
lasso_r2_test  = lasso.score(X_test,y_test)
print("The train R2 for lasso model is", round(lasso_r2_train*100, 2))
print("The test R2 for lasso model is",  round(lasso_r2_test*100, 2))
```

**Step 4**: Get selection results

```python
# Make spec dataframe
lasso_spec = pd.DataFrame()
lasso_spec["feature"] = features
lasso_spec["coef"] = lasso.coef_

# Inspect zero coefs
# Ref: https://stackoverflow.com/a/4588654
lasso_spec.iloc[np.where(lasso_spec["coef"]==0)[0]]
```

### Lasso with Cross Validation

Follow Steps 0-2 from last section, then

**Step 3**: Run LASSO with CV

```python
# Lasso cross validation
lasso_cv = LassoCV(cv=10, random_state=0).fit(X_train, y_train)

# Get R2 values
lasso_cv_r2_train = lasso_cv.score(X_train,y_train)
lasso_cv_r2_test  = lasso_cv.score(X_test,y_test)
print("The train R2 for lasso cv model is", round(lasso_cv_r2_train*100, 2))
print("The test R2 for lasso cv model is",  round(lasso_cv_r2_train*100, 2))

# Get optimal alpha
alpha_best = lasso_cv.alpha_
print("The optimal alpha is", alpha_best)
```

**Step 4**: Run LASSO again with best alpha

```python
# Best Lasso model from cross validation
lasso_best = Lasso(alpha=alpha_best, random_state=0).fit(X_train, y_train)

# Get R2 values
lasso_best_r2_train = lasso_best.score(X_train,y_train)
lasso_best_r2_test  = lasso_best.score(X_test,y_test)
print("The train R2 for best lasso model is", round(lasso_best_r2_train*100, 2))
print("The test R2 for best lasso model is",  round(lasso_best_r2_test*100, 2))
```

**Step 5**: Get selection results

```python
# Make spec dataframe
lasso_best_spec = pd.DataFrame()
lasso_best_spec["feature"] = features
lasso_best_spec["coef"] = lasso_best.coef_

# Inspect zero coefs
# Ref: https://stackoverflow.com/a/4588654
elim = list(lasso_best_spec.iloc[np.where(lasso_best_spec["coef"]==0)[0]]["feature"])

print(elim)
print("The number of eliminated independent variables is", len(elim))
```

### Group Lasso

TBE.

To perform grouped LASSO, see [this question](https://stackoverflow.com/questions/43163418/). I feel like [mathurinm/celer](https://github.com/mathurinm/celer) looks rather promising.

Refs:

- [interpretation - Categorical variables in LASSO regression - Cross Validated](https://stats.stackexchange.com/a/168934)
- [regression coefficients - How to treat categorical predictors in LASSO - Cross Validated](https://stats.stackexchange.com/a/326846)
- [Sparse Group Lasso in Python. A tutorial on how to use one of the… | by Álvaro Méndez Civieta | Towards Data Science](https://towardsdatascience.com/sparse-group-lasso-in-python-255e379ab892)



## Principal Component Analysis \(PCA\)

Refs: 

- [Principal Component Analysis (PCA) in Python Tutorial | DataCamp](https://www.datacamp.com/tutorial/principal-component-analysis-in-python)
- [scikit-learn : Data Compression via Dimensionality Reduction I - Principal component analysis (PCA) - 2020](https://www.bogotobogo.com/python/scikit-learn/scikit_machine_learning_Data_Compresssion_via_Dimensionality_Reduction_1_Principal_component_analysis%20_PCA.php)
- [Principal Component Analysis with Python - GeeksforGeeks](https://www.geeksforgeeks.org/principal-component-analysis-with-python/)


```python
from sklearn.decomposition import PCA

# check shape of original data
imp_iter_df.shape
# (800, 50)

pca = PCA(n_components=2)

pca_df = pd.DataFrame(
    data = pca.fit_transform(imp_qof_s_df),
    columns = ["PC1", "PC2"],
    index = list(df.index),
)

# check shape of pca data
pca_df.shape
# (800, 2)
```
