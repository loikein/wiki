---
weight: 500
title: "Jupyter Notebook/Lab"
---
Everything here is inside a running Python environment.

## Basics

Convert to HTML:

```bash
$ jupyter nbconvert --execute --to html my_notebook.ipynb
```

## Debug

Rebuild lab:

```sh
# takes 1.5 min on my machine:
jupyter lab build
```

## Custom CSS for Lab

For usage see: [Browser extension #Customise the web](/computer/internet/browser-extension/#customise-the-web)

Range: URLs starting with: `http://localhost:8888/lab`

{{< highlight-file file="jupyter-lab.css" lang="css" >}}


## Settings

Refs:

- [jupyterlab/packages/codemirror/src/extension.ts at main · jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab/blob/main/packages/codemirror/src/extension.ts)
- [Advanced Usage — JupyterLab 4.0.6 documentation](https://jupyterlab.readthedocs.io/en/stable/user/directories.html)

### Find paths

```sh
# All paths (same): (some of them may not exit.)
jupyter --path  
jupyter --paths

# config:
#     /Users/loikein/.jupyter
#     /Users/loikein/.local/etc/jupyter
#     /usr/local/Caskroom/miniconda/base/envs/google-maps/etc/jupyter
#     /usr/local/etc/jupyter
#     /etc/jupyter
# data:
#     /Users/loikein/Library/Jupyter
#     /Users/loikein/.local/share/jupyter
#     /usr/local/Caskroom/miniconda/base/envs/google-maps/share/jupyter
#     /usr/local/share/jupyter
#     /usr/share/jupyter
# runtime:
#     /Users/loikein/Library/Jupyter/runtime
```

```sh
# Only lab paths:
jupyter lab path

# Application directory:   /usr/local/Caskroom/miniconda/base/envs/google-maps/share/jupyter/lab
# User Settings directory: /Users/loikein/.jupyter/lab/user-settings
# Workspaces directory: /Users/loikein/.jupyter/lab/workspaces
```

Generate top level config file: \([credit](https://stackoverflow.com/a/50750181/10668706)\)

```sh
jupyter lab --generate-config
# Writing default config to: /Users/loikein/.jupyter/jupyter_lab_config.py
```

### `page_config.json` \(user-level\) \(deprecated\)

{{< details "This config method is deprecated." >}}
Doc: [Advanced Usage — JupyterLab 4.0.6 documentation #page_config.json (deprecated)](https://jupyterlab.readthedocs.io/en/stable/user/directories.html#page-config-json-deprecated)

Credit: [jupyterlab/jupyterlab Issue #9240](https://github.com/jupyterlab/jupyterlab/issues/9240#issuecomment-718966268)

```sh
jupyter labextension disable @jupyterlab/launcher-extension
jupyter labextension enable @jupyterlab/launcher-extension
```

Then I got: `/usr/local/Caskroom/miniconda/base/envs/google-maps/etc/jupyter/labconfig/page_config.json` with the following content:

```json
{
  "disabledExtensions": {
    "@jupyterlab/launcher-extension": false
  }
}
```
{{< /details >}}


### `overrides.json` \(environment-level\)

> You can override default values of the extension settings by defining new default values in an `overrides.json` file. For example, if you would like to override the default theme to be the dark theme, create an `overrides.json` file containing the following lines in the [application settings directory](https://jupyterlab.readthedocs.io/en/stable/user/directories.html#application-settings-directory) (for example, if the [JupyterLab Application Directory](https://jupyterlab.readthedocs.io/en/stable/user/directories.html#application-directory) is `<sys.prefix>/local/share/jupyter/lab`, create this file at `<sys.prefix>/local/share/jupyter/lab/settings/overrides.json`).
> 
> ```json
> {
>  "@jupyterlab/apputils-extension:themes": {
>  "theme": "JupyterLab Dark"
>  }
> }
> ```
> 
> ~ [Advanced Usage — JupyterLab 4.0.6 documentation #overrides.json](https://jupyterlab.readthedocs.io/en/stable/user/directories.html#overrides-json)


### `jupyterlab-settings` \(user-level\)

> The user settings directory contains the user-level settings for Jupyter extensions.
> 
> By default, the location is `$HOME/.jupyter/lab/user-settings/`, where `$HOME` is the user’s home directory. This folder is not in the JupyterLab application directory because these settings are typically shared across Python environments. The location can be modified using the `JUPYTERLAB_SETTINGS_DIR` environment variable.
> 
> [JSON5](https://json5.org/) files are automatically created in this folder recording the settings changes a user makes in the JupyterLab Advanced Settings Editor. The file names follow the pattern of `<extension_name>/<plugin_name>.jupyterlab-settings`. **These values override the default values given by extensions, as well as the default overrides from the [overrides.json](https://jupyterlab.readthedocs.io/en/stable/user/directories.html#overridesjson) file** in the application’s settings directory.
> 
> ~ [Advanced Usage — JupyterLab 4.0.6 documentation #JupyterLab User Settings Directory](https://jupyterlab.readthedocs.io/en/stable/user/directories.html#jupyterlab-user-settings-directory)



## Useful Notebook Extensions

Doc: [Extensions — JupyterLab 4.0.6 documentation](https://jupyterlab.readthedocs.io/en/stable/user/extensions.html)

```sh
jupyter labextension list

# JupyterLab v4.0.5
# /usr/local/Caskroom/miniconda/base/envs/google-maps/share/jupyter/labextensions
#         jupyterlab-jupytext v1.3.9 enabled  X (python, jupytext)
#         jupyterlab_pygments v0.2.2 enabled  X (python, jupyterlab_pygments)
#         jupyterlab-execute-time v3.0.1 enabled OK (python, jupyterlab_execute_time)
```

