---
title: "Git"
---

# Git

References:

- [Version Control (Git) · the missing semester of your cs education](https://missing.csail.mit.edu/2020/version-control/)
- [Git - Reference](https://git-scm.com/docs)

Basic terms:

- tree: folder
- blob: file
- HEAD: the current state that you're looking at
- stage: telling git about the changes
- commit: record the staged changes

## Useful Aliases

### Oh-My-Zsh Git Plugin

References:

- [Cheatsheet · ohmyzsh/ohmyzsh Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Cheatsheet#git)
- [Oh-My-Zsh Git Aliases](https://jasonm23.github.io/oh-my-git-aliases.html)

```shell
# git status
gst

# git pull
gl

# git push
gp

# git checkout master
gcm

# git commit -m
gcmsg "message here"

# All cached changes
# git diff --cached
# git diff --staged
gds

# git diff --word-diff
gdw
```

### Others

Reference: [Git - git-log Documentation](https://git-scm.com/docs/git-log)

In `~/.zshrc`: \(`tformat` is preferred over `format`, [credit](https://stackoverflow.com/a/9007395)\)

```shell
# Use languages other than default shell language
alias git='LANG="zh_CN.UTF-8" git'
# Very pretty log
alias glog="git log --graph --full-history --all --date=short --pretty=tformat:'%Cred%h%Creset %C(bold green)%ad%Creset %s %C(yellow)%d%Creset %Cblue<%an>%Creset'"
```

Or set from shell directly: \(cannot overwrite default commands\) \([credit](https://strivingboy.github.io/blog/2014/09/29/better-git-log/)\)

```shell
git config --global alias.lg "log --graph --full-history --all --date=short --pretty=tformat:'%Cred%h%Creset %C(bold green)%ad%Creset %s %C(yellow)%d%Creset %Cblue<%an>%Creset'"
```

## Observe Things

### Diff & Plot Graph

Difference between most recent commit and second most recent commit: \([credit](https://stackoverflow.com/a/9903611/10668706)\)

```shell
git diff HEAD^ HEAD
```

Difference between branches: \([credit](https://stackoverflow.com/a/9834872)\)

```shell
git diff branch_1..branch_2
```

Difference between staged \(added\) changes and most recent commit:

```shell
git diff --staged
```

Show all files under git version control:

```shell
# r for recursive
git ls-tree -r --full-tree --name-only HEAD
# or
git ls-files
```

Find out how many files are being tracked: \([credit](https://stackoverflow.com/a/9468981/10668706)\)

```shell
# All files
git ls-files | wc -l

# Some kind of file (e.g. Markdown)
git ls-files | grep "\.md$" | wc -l
```

### Blame

Reference: [Git - git-blame Documentation](https://git-scm.com/docs/git-blame)

```shell
# Inspect lines 20~30
git blame a-file.md -L 20,30

# Inspect from start of file to line 30
git blame a-file.md -L ,30

# Inspect from line 20 to end of file
git blame a-file.md -L 20,
```

### Remote

Show all remote URLs:

```shell
git remote --verbose
git remote -v
```

## Commit-Level Operations

Interactive chunk-staging:

```shell
git add --patch somefile.txt
git add -p somefile.txt
```

Change last commit message:

```shell
git commit --amend
```

Gently squash last two \(or any number of\) commits: \([credit](https://stackoverflow.com/a/5201642)\)

```shell
git reset --soft HEAD~2
git commit --edit -m"$(git log --format=%B --reverse HEAD..HEAD@{1})"
```

Undo last commit: \([credit](https://stackoverflow.com/a/927386)\)

```shell
git reset HEAD~1
```

### Apply Late `.gitignore`

Commit first:

```shell
git commit -m "add/change .gitignore"
subl .gitignore
```

Add something to `.gitignore`, for example:

```text
# Things to ignore
**/.DS_Store
**/*.pdf

# Things to keep
!roadmap.pdf
```

Apply changes:

```shell
git rm -r --cached . && git add . && git commit -m "apply .gitignore"
```

### `git bisect`

TBA

## Repository-Level Operations

### Pull Updates from Origin of Fork

Ref: [git - Pull new updates from original GitHub repository into forked GitHub repository - Stack Overflow](https://stackoverflow.com/a/3903835/10668706)

Scenario: I have a forked repository on GitHub, cloned to local machine, and want to pull the updates from the original repository.

Add original repository as remote, call it `upstream`: \(the name does not matter, can even call it `spoon`\)

```shell
git remote add upstream https://github.com/something/something.git
git fetch upstream
```

If want to keep all fork commits:

```shell
git merge upstream/master master
```

If want clean commit history:

```shell
git rebase upstream/master
```

### Branches

See all branches:

```shell
git branch

# See some more info
git branch --verbose
git branch -v
```

Create branch:

```shell
git branch my-new-branch
git checkout my-new-branch

# or
git checkout -b my-new-branch
```

Change branch name:

```shell
git branch -m master main
git push -u origin main

# external action required: go to origin (e.g. GitHub)
# and change the default branch

git push origin --delete master
```

Move files changes to another branch: \([credit](https://stackoverflow.com/a/35742820)\)

```shell
# p for patch
git checkout <other_branch_name> <files/to/grab in/list/separated/by/spaces> -p
```

Merge master to new branch: ([credit](https://stackoverflow.com/questions/16955980/git-merge-master-into-feature-branch#comment83176031_16957483))

```shell
git pull origin master
```

Delete local branch:

```shell
git checkout master
git branch -d my-old-branch
```

Delete all gone local branches: \([credit](https://stackoverflow.com/a/28464339)\)

```shell
git remote prune origin
```

<!--
\([credit](https://medium.com/@kcmueller/delete-local-git-branches-that-were-deleted-on-remote-repository-b596b71b530c)\)

```shell
# Pull newest version
git fetch --prune origin

# Delete all gone branches
git branch -v | grep ': gone]'|  grep -v "\*" | awk '{ print $1; }' | xargs -r git branch -d
``` -->

Delete remote branch:

```shell
git push -d origin my-old-branch
```

### Merge Master into Branch

Credit: GitHub

```shell
# From your project repository, bring in the changes and test.
git fetch origin
git checkout -b "my-branch" "origin/my-branch"
git merge "master"

# Merge the changes and update on remote.
git checkout "master"
git merge --no-ff "my-branch"
git push origin "master"
```

## Split Repo

Credit: [git subtree - Detach (move) subdirectory into separate Git repository - Stack Overflow](https://stackoverflow.com/a/17864475)

```shell
# Prepare the old repo
cd <big-repo>
git subtree split -P <name-of-folder> -b <name-of-new-branch>

# Create new repo
mkdir ~/<new-repo> && cd ~/<new-repo>
git init
git pull </path/to/big-repo> <name-of-new-branch>

# Clean old repo
cd <big-repo>
git rm -rf <name-of-folder>
```

## Submodule

### Add

Credit [1](https://stackoverflow.com/a/15782629), [2](https://stackoverflow.com/a/55885186)

```shell
# Default branch
git submodule add <remote-URL>

# Specify branch
git submodule add -b <branch-name> <remote-URL> <preferred-folder-name>

# Track a specific branch after init
git submodule set-branch --branch <branch-name> <folder-name>
```

Initial pull submodule:

```shell
git submodule update --init --recursive
```

### Update (Fetch)

Update all submodules: \([credit](https://www.vogella.com/tutorials/GitSubmodules/article.html#submodules_pulling)\)

```shell
git submodule update --remote
```

Show list of all submodules: \([credit](https://stackoverflow.com/a/54238999)\)

```shell
# Either will work
git ls-tree -r HEAD
git submodule status
```

### Edit

Make changes to submodules without committing: (in `.gitmodules`)

```diff
[submodule "something"]
    path = something
    url = https://github.com/something/something.git
+   ignore = untracked
```

Change the directory name for a submodule: \([credit](https://stackoverflow.com/a/5540263/10668706)\)

1. Update `.gitmodules`.
1. Run `git add .gitmodules`
1. Run `git mv /path/to/old/directory /path/to/new/directory`
1. Run `git add .`

Change remote URL for a submodule: \([credit](https://stackoverflow.com/a/914135)\)

```shell
git submodule set-url <path> <newurl>
```

### Remove

The easy way: `git rm <path-to-submodule>`

The hard way: \([credit](https://stackoverflow.com/a/1260982)\)

1. Delete the relevant section from the `.gitmodules` file.
1. `git add .gitmodules`
1. Delete the relevant section from `.git/config`.
1. `git rm --cached <path-to-submodule>`
1. `rm -rf .git/modules/<path-to-submodule>`
1. `rm -rf <path-to-submodule>`

## Pre-Commit

## Git Flow

References:

- [Learn Version Control with Git - Workflows with git-flow](https://www.git-tower.com/learn/git/ebook/en/command-line/advanced-topics/git-flow) \([中文版](https://www.git-tower.com/learn/git/ebook/cn/command-line/advanced-topics/git-flow)\)
- [petervanderdoes/gitflow-avh: AVH Edition of the git extensions to provide high-level repository operations for Vincent Driessen's branching model](https://github.com/petervanderdoes/gitflow-avh)
- [Command Line Arguments · nvie/gitflow Wiki](https://github.com/nvie/gitflow/wiki/Command-Line-Arguments)

Installation:

```shell
brew install git-flow-avh
```

Initialise: (`-d` means using default branch names)

```shell
git flow init -d
```

Write new feature:

```shell
# Before beginning
git flow feature start my-new-feature

# After final commit
git flow feature finish my-new-feature
```

## Debugging

### Repository not found.

Don't have write access. Ask a maintainer/admin to add you as contributor.

### How to find whether I have write access?

In browser, open a random file of the repository, and hit the edit button. If can edit, then have write access. \([credit](https://stackoverflow.com/a/40326507)\)

### refusing to allow an OAuth App to create or update workflow

Use token to login.

1. Sign out from git
    - Open `Keychain Access.app`, delete the Internet password for `github.com`, or
    - `git config --global --unset credential.helper`
1. Push again, and when prompted to enter password, enter a personal access token.
