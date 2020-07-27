# Anaconda/Miniconda

References:

- [conda 4.8.3.post170+49783e80 documentation](https://docs.conda.io/projects/conda/en/latest/index.html)
- [CONDA 4.6 CHEAT SHEET](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf)
- [CONDA CHEAT SHEET](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf)

## Managing Environments

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
