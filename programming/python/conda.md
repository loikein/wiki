# Anaconda/Miniconda

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

## Managing Packages

### Force Re-installation

Force reinstalling:

```bash
$ conda install numpy --force-reinstall
```

If that doesn't work:

1. Open conda's package directories. (example: Miniconda)
    - `/opt/miniconda3/pkgs/`
    - `/opt/miniconda3/envs/my-env/lib/python3.7/site-packages/`
1. Remove the package.
1. Run `conda env update`.

If that doesn't work:

1. Switch to base environment or run `conda deactivate`
1. Delete `my-env` with `conda remove -n my-env --all -y`
1. Create it again with `conda env create -f environment.yml`
