---
weight: 100
title: "Conda/Mamba"
---

References:

- [conda 4.8.3.post170+49783e80 documentation](https://docs.conda.io/projects/conda/en/latest/index.html)
- [CONDA 4.6 CHEAT SHEET](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf)
- [CONDA CHEAT SHEET](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf)

## Managing Environments

Toggling channel priority:

```bash
# see the current setting
$ conda config --describe channel_priority

# set to flexible if environment conflict just won't resolve
$ conda config --set channel_priority flexible

# set to strict if feeling lucky
$ conda config --set channel_priority strict
```

Create an environment from file:

```bash
$ conda env create --file environment.yml
$ conda env create -f environment.yml
```

Update an environment:

```bash
$ conda env update
```

Delete an environment:

```bash
$ conda remove --name my-env --all --yes
$ conda remove -n my-env --all -y
```

### Manage Jupyter Notebook Installation

```yaml
dependencies:
  - ipykernel

  # If need Jupyter Lab
  - jupyterlab

  # If need extensions
  - jupyter_contrib_nbextensions
  … (List of extensions that need installation)
```

## Managing Packages

### Check Package Version

```bash
$ conda list --full-name <package-name>
```

### Force Re-installation

First, deactivate the current environment and activate again.

If that doesn't work:

```bash
$ conda install --force-reinstall <a-bad-package>
```

If that doesn't work:

1. Open conda's package directories. (example: Miniconda)
    - Check: `conda info`
    - `/opt/miniconda3/pkgs/`
    - `/opt/miniconda3/envs/my-env/lib/python3.7/site-packages/`
1. Remove the package.
1. Run `conda env update`.

If that doesn't work:

1. Switch to base environment or run `conda deactivate`
1. Delete `my-env` with `conda remove -n my-env --all -y`
1. Create it again with `conda env create -f environment.yml`


## Magic commands

Doc: [Built-in magic commands — IPython 8.21.0 documentation](https://ipython.readthedocs.io/en/stable/interactive/magics.html)

### System commands

```python
# Prints current working directory
%pwd
```

### Show function definition

Ref: [Can Python print a function definition? - Stack Overflow](https://stackoverflow.com/a/1562772/10668706)

```python
# help
function_name?

# definition
function_name??
```


## Use with direnv

### Auto activate environment

`.envrc`:

```sh
cd /usr/local/Caskroom/miniconda/base/bin
source activate myenv
cd -
```

### Use local package

`.envrc`:

```sh
export PROJECT_ROOT=$PWD
export PYTHONPATH=$PROJECT_ROOT:$PYTHONPATH # prioritise local packages
```

The environment directory must look like this:

```text
.
├── .envrc
├── environment.yml
├── my_package
│   ├── __init__.py
│   └── ...
└── ...
```
