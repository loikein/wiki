# Example Project Flow

Previously posted on [Notes on Effective Programming Practice - loikein's notes](https://notes.loikein.one/post/2019/10/notes-effective-programming/).

## Clone from Remote

```bash
# clone
$ git clone https://github.com/path-to-your-repo

# new branch
$ git branch loikein
$ git checkout loikein

$ subl .gitignore
# add:
# **/.DS_Store

# pre-commit hooks
$ pre-commit install
$ pre-commit run

# creat an environment from an environment.yml file
$ conda env create -f environment.yml
$ conda activate exercise_x

$ python waf.py configure
```

## Create from Local

```bash
# init
$ git init

$ subl .gitignore
# add:
# **/.DS_Store

# pre-commit hooks
$ pre-commit install
$ pre-commit run

$ git add --all
$ git commit -m "Init commit"

# after creating empty repository on GitHub

$ git remote add origin https://github.com/loikein/tofu-output-beautifier.git
$ git push -u origin master

# creat an environment from an environment.yml file
$ conda env create -f environment.yml
$ conda activate exercise_x

$ python waf.py configure
```

## Create from cookiecutter

```bash
# if does not have cookiecutter
$ brew install cookiecutter

$ cookiecutter https://github.com/OpenSourceEconomics/econ-project-templates/archive/v0.3.2.zip
# check sphinx for document

$ conda activate exercise_x

$ subl .gitignore
# add:
# **/.DS_Store

$ pre-commit install

$ python waf.py configure
$ python waf.py build -v
$ python waf.py install

# if have set remote url
$ git pull origin master --allow-unrelated-histories
$ git push --set-upstream origin master

# new branch
$ git branch loikein
$ git checkout loikein
```
