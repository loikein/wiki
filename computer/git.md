# Git

## General

Difference between most recent commit and second most recent commit: ([credit](https://stackoverflow.com/a/9903611/10668706))

```bash
$ git diff HEAD^ HEAD
```

Difference between staged changes and most recent commit:

```bash
$ git diff --cached
```

Show remote URL:

```bash
$ git remote show origin
```
Change last commit message:

```bash
$ git commit --amend
```

Show the file tree under git version control:

```bash
$ git ls-tree --full-tree -r --name-only HEAD
```

Gently squash last two commits:

```bash
# Commit first!!
$ git reset --soft HEAD~2
$ git commit --edit -m"$(git log --format=%B --reverse HEAD..HEAD@{1})"
```

### Oh-My-Zsh Aliases

References:

- [Cheatsheet · ohmyzsh/ohmyzsh Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Cheatsheet#git)
- [Oh-My-Zsh Git Aliases](https://jasonm23.github.io/oh-my-git-aliases.html)

```bash
# git status
$ gst

# git pull
$ gl

# git push
$ gp

# git checkout master
$ gcm

# git commit -m
$ gcmsg "message here"
```

## `.gitignore`

Add late ignore:

```bash
$ git commit -m "add/change .gitignore"
$ subl .gitignore
```

In `.gitignore`:

```text
# Things to ignore
**/.DS_Store
**/*.pdf

# Things to keep
!roadmap.pdf
```

Apply changes:

```bash
$ git rm -r --cached . && git add . && git commit -m ".gitignore is now working"
```

## Branches

Create branch:

```bash
$ git branch my-new-branch
$ git checkout my-new-branch
```

Merge master to new branch: ([credit](https://stackoverflow.com/questions/16955980/git-merge-master-into-feature-branch#comment83176031_16957483))

```bash
$ git pull origin master
```

Delete local branch:

```bash
$ git checkout master
$ git branch -d my-old-branch
```

Delete remote branch:

```bash
$ git push -d origin my-old-branch
```

## Submodules

Add submodule:

```bash
$ git submodule add https://github.com/something/something.git
```

Initial pull submodule:

```bash
$ git submodule update --init --recursive
```

Update all submodules: \([credit](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules)\)

```bash
$ git submodule update --recursive --remote

# or
$ git submodule -q foreach git pull -q origin master
```

In `.gitmodules`:

```text
[submodule "something"]
    path = something
    url = https://github.com/something/something.git
+    ignore = untracked
```

## Git Flow

References:

- [Learn Version Control with Git - Workflows with git-flow](https://www.git-tower.com/learn/git/ebook/en/command-line/advanced-topics/git-flow) ([中文版](https://www.git-tower.com/learn/git/ebook/cn/command-line/advanced-topics/git-flow))
- [petervanderdoes/gitflow-avh: AVH Edition of the git extensions to provide high-level repository operations for Vincent Driessen's branching model](https://github.com/petervanderdoes/gitflow-avh)
- [Command Line Arguments · nvie/gitflow Wiki](https://github.com/nvie/gitflow/wiki/Command-Line-Arguments)

Installation:

```bash
$ brew install git-flow-avh
```

Initialise: (`-d` means using default branch names)

```bash
$ git flow init -d
```

Write new feature:

```bash
# Before beginning
$ git flow feature start my-new-feature

# After final commit
$ git flow feature finish my-new-feature
```
