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

# All cached changes
# git diff --cached
# git diff --staged
$ gds
```

### Others

Reference: [Git - git-log Documentation](https://git-scm.com/docs/git-log)

In `~/.zshrc`: \(`tformat` is preferred over `format`, [credit](https://stackoverflow.com/a/9007395)\)

```bash
# Use languages other than default shell language
alias git='LANG="zh_CN.UTF-8" git'
# Very pretty log
alias glog="git log --graph --full-history --all --date=short --pretty=tformat:'%Cred%h%Creset %C(bold green)%ad%Creset %s %C(yellow)%d%Creset %Cblue<%an>%Creset'"
```

Or set from shell directly: \(cannot overwrite default commands\) \([credit](https://strivingboy.github.io/blog/2014/09/29/better-git-log/)\)

```bash
$ git config --global alias.lg "log --graph --full-history --all --date=short --pretty=tformat:'%Cred%h%Creset %C(bold green)%ad%Creset %s %C(yellow)%d%Creset %Cblue<%an>%Creset'"
```

## Observe Things

### Diff & Plot Graph

Difference between most recent commit and second most recent commit: \([credit](https://stackoverflow.com/a/9903611/10668706)\)

```bash
$ git diff HEAD^ HEAD
```

Difference between staged \(added\) changes and most recent commit:

```bash
$ git diff --staged
```

Show all files under git version control:

```bash
# r for recursive
$ git ls-tree -r --full-tree --name-only HEAD
# or
$ git ls-files
```

Find out how many files are being tracked: \([credit](https://stackoverflow.com/a/9468981/10668706)\)

```bash
# All files
$ git ls-files | wc -l

# Some kind of file (e.g. Markdown)
$ git ls-files | grep "\.md$" | wc -l
```

### Remote

Show all remote URLs:

```bash
$ git remote --verbose
$ git remote -v
```

## Commit-Level Operations

Interactive chunk-staging:

```bash
$ git add --patch somefile.txt
$ git add -p somefile.txt
```

Change last commit message:

```bash
$ git commit --amend
```

Gently squash last two \(or any number of\) commits: \([credit](https://stackoverflow.com/a/5201642)\)

```bash
$ git reset --soft HEAD~2
$ git commit --edit -m"$(git log --format=%B --reverse HEAD..HEAD@{1})"
```

### Apply Late `.gitignore`

Commit first:

```bash
$ git commit -m "add/change .gitignore"
$ subl .gitignore
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

```bash
$ git rm -r --cached . && git add . && git commit -m "apply .gitignore"
```

### `git bisect`

TBA

## Repository-Level Operations

### Pull Updates from Origin of Fork

Ref: [git - Pull new updates from original GitHub repository into forked GitHub repository - Stack Overflow](https://stackoverflow.com/a/3903835/10668706)

Scenario: I have a forked repository on GitHub, cloned to local machine, and want to pull the updates from the original repository.

Add original repository as remote, call it `upstream`: \(the name does not matter, can even call it `spoon`\)

```bash
$ git remote add upstream https://github.com/something/something.git
$ git fetch upstream
```

If want to keep all fork commits:

```bash
$ git merge upstream/master master
```

If want clean commit history:

```bash
$ git rebase upstream/master
```

### Branches

See all branches:

```bash
$ git branch

# See some more info
$ git branch --verbose
$ git branch -v
```

Create branch:

```bash
$ git branch my-new-branch
$ git checkout my-new-branch

# or
$ git checkout -b my-new-branch
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

Delete all gone local branches: \([credit](https://medium.com/@kcmueller/delete-local-git-branches-that-were-deleted-on-remote-repository-b596b71b530c)\)

```bash
# Pull newest version
$ git fetch --prune origin

# Delete all gone branches
$ git branch -v | grep ': gone]'|  grep -v "\*" | awk '{ print $1; }' | xargs -r git branch -d
```

Delete remote branch:

```bash
$ git push -d origin my-old-branch
```

### Merge Master into Branch

Credits: [1](https://stackoverflow.com/questions/16955980/git-merge-master-into-feature-branch#comment66136906_16957483), [2](https://gist.github.com/santisbon/a1a60db1fb8eecd1beeacd986ae5d3ca)

```bash
# Pull newest version
$ git fetch

# Do the merge
$ git merge origin/master

# If any conflict appears, solve it…

# Finally
$ git commit
```

## Submodule

### Add

```bash
$ git submodule add https://github.com/something/something.git
```

Initial pull submodule:

```bash
$ git submodule update --init --recursive
```

### Update (Fetch)

Update all submodules: \([credit](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules#comment9839868_1032653)\)

```bash
$ git submodule -q foreach git pull -q origin master
```

Show list of all submodules without entering less: \([credit](https://stackoverflow.com/a/12641787)\)

```bash
$ git config --file .gitmodules --get-regexp path | awk '{ print $2 }'
```

### Edit

Make changes to submodules without committing: (in `.gitmodules`)

```text
[submodule "something"]
    path = something
    url = https://github.com/something/something.git
+    ignore = untracked
```

Change the directory name for a submodule: \([credit](https://stackoverflow.com/a/5540263/10668706)\)

1. Update `.gitmodules`.
1. Run `git add .gitmodules`
1. Run `git mv /path/to/old/directory /path/to/new/directory`
1. Run `git add .`

### Remove

Reference: [github - What is the current way to remove a git submodule? - Stack Overflow](https://stackoverflow.com/questions/29850029/what-is-the-current-way-to-remove-a-git-submodule)

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
