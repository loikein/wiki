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

## LASSO

Refs:

- [Lasso and Ridge Regression in Python Tutorial | DataCamp](https://www.datacamp.com/tutorial/tutorial-lasso-ridge-regression)
- [Lasso Regression with Python | Jan Kirenz](https://www.kirenz.com/post/2019-08-12-python-lasso-regression-auto/)



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
