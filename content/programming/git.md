---
title: "Git"
---

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

- All aliases: [ohmyzsh/plugins/git/git.plugin.zsh at master · ohmyzsh/ohmyzsh](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/git/git.plugin.zsh#L67)
- [Cheatsheet · ohmyzsh/ohmyzsh Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Cheatsheet#git)

```sh
# git status
gst

# git pull
gl

# git push
gp

# git checkout master/main
gcm

# git commit -m
gcmsg "message here"

# All cached changes
# git diff --cached
# git diff --staged
gds

# git diff --word-diff
gdw

# git log --oneline --decorate --graph
glog

# git remote --verbose
grv
```

### Change git CLI language

Does not work in tmux for reasons unknown.

In `~/.zshrc`:

```sh
# Use languages other than default shell language
alias git='LANG="zh_CN.UTF-8" git'
```

## Observe Things

### Logs

See all files changed with each commit: \([credit](https://stackoverflow.com/a/49854517)\)

```sh
git log --stat
```

One-line graphic log: \(credits: [new](https://stackoverflow.com/a/35075021), [old](https://strivingboy.github.io/blog/2014/09/29/better-git-log)\); \(`tformat` is preferred over `format`, see [credit](https://stackoverflow.com/a/9007395)\)

```sh
git log --all --decorate --oneline --graph

# old version:
git log --graph --full-history --all --date=short --pretty=tformat:'%Cred%h%Creset %C(bold green)%ad%Creset %s %C(yellow)%d%Creset %Cblue<%an>%Creset'
```

### Diff

Difference between most recent commit and second most recent commit: \([credit](https://stackoverflow.com/a/9903611/10668706)\)

```sh
git diff HEAD^ HEAD
```

Difference between branches: \([credit](https://stackoverflow.com/a/9834872)\)

```sh
git diff branch_1..branch_2
```

Difference between staged \(added\) changes and most recent commit:

```sh
git diff --staged
```

Only list changed file names and status: \([Doc](https://git-scm.com/docs/git-diff): Added (`A`), Copied (`C`), Deleted (`D`), Modified (`M`), Renamed (`R`), have their type (i.e. regular file, symlink, submodule, …) changed (`T`), are Unmerged (`U`), are Unknown (`X`), or have had their pairing Broken (`B`)\)

```sh
git diff --name-status <commit>
```

### Files

Show all files under git version control:

```sh
# r for recursive
git ls-tree -r --full-tree --name-only HEAD
# or
git ls-files
```

Find out how many files are being tracked: \([credit](https://stackoverflow.com/a/9468981/10668706)\)

```sh
# All files
git ls-files | wc -l

# Some kind of file (e.g. Markdown)
git ls-files | grep "\.md$" | wc -l
```

### Blame

Reference: [Git - git-blame Documentation](https://git-scm.com/docs/git-blame)

```sh
# Inspect lines 20~30
git blame a-file.md -L 20,30

# Inspect from start of file to line 30
git blame a-file.md -L ,30

# Inspect from line 20 to end of file
git blame a-file.md -L 20,
```

### Remote

Show all remote URLs:

```sh
git remote --verbose
git remote -v
```

## Commit-Level Operations

Interactive chunk-staging:

```sh
git add --patch somefile.txt
git add -p somefile.txt
```

Change last commit message:

```sh
git commit --amend
```

Gently squash last two \(or any number of\) commits: \([credit](https://stackoverflow.com/a/5201642)\)

```sh
git reset --soft HEAD~2
git commit --edit -m"$(git log --format=%B --reverse HEAD..HEAD@{1})"
```

Undo last commit: \([credit](https://stackoverflow.com/a/927386)\)

```sh
git reset HEAD~1
```

### Apply Late `.gitignore`

Commit first:

```sh
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

```sh
git rm -r --cached . && git add . && git commit -m "apply .gitignore"
```

### `git bisect`

TBA

## Repository-Level Operations

### Branches

See all branches:

```sh
git branch

# See some more info
git branch --verbose
git branch -v
```

Create branch:

```sh
git branch my-new-branch
git checkout my-new-branch

# or
git checkout -b my-new-branch
```

Change branch name:

```sh
git branch -m master main
git push -u origin main

# external action required: go to origin (e.g. GitHub)
# and change the default branch

git push origin --delete master
```

Move files changes to another branch: \([credit](https://stackoverflow.com/a/35742820)\)

```sh
# p for patch
git checkout <other_branch_name> <files/to/grab in/list/separated/by/spaces> -p
```

Merge master to new branch: ([credit](https://stackoverflow.com/questions/16955980/git-merge-master-into-feature-branch#comment83176031_16957483))

```sh
git pull origin master
```

Delete local branch:

```sh
git checkout master
git branch -d my-old-branch
```

Delete all gone local branches: \([credit](https://stackoverflow.com/a/28464339)\)

```sh
git remote prune origin
```

<!--
\([credit](https://medium.com/@kcmueller/delete-local-git-branches-that-were-deleted-on-remote-repository-b596b71b530c)\)

```sh
# Pull newest version
git fetch --prune origin

# Delete all gone branches
git branch -v | grep ': gone]'|  grep -v "\*" | awk '{ print $1; }' | xargs -r git branch -d
``` -->

Delete remote branch:

```sh
git push -d origin my-old-branch
```

### Merge Master into Branch

Credit: GitHub

```sh
# From your project repository, bring in the changes and test.
git fetch origin
git checkout -b "my-branch" "origin/my-branch"
git merge "master"

# Merge the changes and update on remote.
git checkout "master"
git merge --no-ff "my-branch"
git push origin "master"
```

### Remove sensitive data from history

Haven't tried: 
[Removing sensitive data from a repository - GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

## Split Repo

Credit: [git subtree - Detach (move) subdirectory into separate Git repository - Stack Overflow](https://stackoverflow.com/a/17864475)

```sh
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

## Fork related operations

### Pull Updates from Origin of Fork

Ref: [git - Pull new updates from original GitHub repository into forked GitHub repository - Stack Overflow](https://stackoverflow.com/a/3903835/10668706)

#### Keep own changes

Scenario: I have a forked repository on GitHub, and want to pull the updates from the original repository, while keeping my own changes.

<u>Step 1</u>: Clone to local machine.

<u>Step 2</u>: Add original repository as remote \(the name does not matter, can even call it `spoon`\)

```sh
git remote add upstream https://github.com/something/something.git
git fetch upstream
```

<u>Step 3</u>: Open a new branch \(optional\)

If it takes a long time to resolve all the merge conflicts, this step will preserve the main branch for production until merge is ready.

```sh
git checkout -b merge-upstream main
git checkout -b merge-upstream master
```

<u>Step 4</u>: Run merge

If want to keep all fork commits:

```sh
git merge upstream/main main
git merge upstream/master master
# or with step 3
git merge upstream/main merge-upstream
git merge upstream/master merge-upstream
```

If want clean commit history:

```sh
git rebase upstream/main
git rebase upstream/master
```

Resolve any conflict, and commit.

<u>Step 5</u>: Merge new branch to main \(optional\)

Needed if have used Step 3.

```sh
git checkout main
git checkout master

git merge merge-upstream
git branch -d merge-upstream
```

Done.

#### Use everything upstream

Scenario: I have used Vercel Deploy Button and now having a private non-fork repository. I did not change anything and only want to stick to the upstream.

First clone it to local machine.

Add original repository as remote, call it `upstream`: \(the name does not matter, can even call it `spoon`\)

<u>Step 1</u>: Clone to local machine.

<u>Step 2</u>: Add original repository as remote, call it `upstream`: \(the name does not matter, can even call it `spoon`\)

```sh
git remote add upstream https://github.com/something/something.git
git fetch upstream
```

<u>Step 3</u>: Run merge

```sh
# resolve all conflicts using upstream code:
# https://stackoverflow.com/a/10697551
git merge upstream/main main --allow-unrelated-histories --strategy-option theirs
```

Done.

### Contribute selected code to fork

<u>Step 1</u>: Add upstream and pull

<u>Step 2</u>: Make branch based on upstream

```sh
git checkout -b fix-1 upstream/main
git checkout -b fix-1 upstream/master
```

<u>Step 3</u>: Change the files and commit

<u>Step 4</u>: Push to own remote fork

```sh
git push origin fix-1
```

<u>Step 5</u>: Create PR with `https://github.com/<original/repo>/pull/new/fix-1`

Done.


## Submodule

### Add

Credit [1](https://stackoverflow.com/a/15782629), [2](https://stackoverflow.com/a/55885186)

```sh
# Default branch
git submodule add <remote-URL>

# Specify branch
git submodule add -b <branch-name> <remote-URL> <preferred-folder-name>

# Track a specific branch after init
git submodule set-branch --branch <branch-name> <folder-name>
```

Initial pull submodule:

```sh
git submodule update --init --recursive
```

### Update (Fetch)

Update all submodules: \([credit](https://www.vogella.com/tutorials/GitSubmodules/article.html#submodules_pulling)\)

```sh
git submodule update --remote
```

Show list of all submodules: \([credit](https://stackoverflow.com/a/54238999)\)

```sh
# Either will work
git ls-tree -r HEAD
git submodule status
```

### Edit

Make changes to submodules (in `.gitmodules`), then do `git submodule update --init --recursive --remote` \([credit](https://stackoverflow.com/a/66200354)\)

```diff
[submodule "something"]
    path = something
    url = https://github.com/something/something.git
+   ignore = untracked
+   branch = new-branch
```

Change the directory name for a submodule: \([credit](https://stackoverflow.com/a/5540263/10668706)\)

1. Update `.gitmodules`.
1. Run `git add .gitmodules`
1. Run `git mv /path/to/old/directory /path/to/new/directory`
1. Run `git add .`

Change remote URL for a submodule: \([credit](https://stackoverflow.com/a/914135)\)

```sh
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

```sh
brew install git-flow-avh
```

Initialise: (`-d` means using default branch names)

```sh
git flow init -d
```

Write new feature:

```sh
# Before beginning
git flow feature start my-new-feature

# After final commit
git flow feature finish my-new-feature
```

## Debugging

### UTF-8 character in filename are displayed in numbers

```sh
git config --global core.quotepath false
```

### Repository not found.

Don't have write access to remote repository. Ask a maintainer/admin to add you as contributor.

### How to find whether I have write access?

In browser, open a random file of the repository, and hit the edit button. If can edit, then have write access. \([credit](https://stackoverflow.com/a/40326507)\)

### refusing to allow an OAuth App to create or update workflow

Use token to login.

1. Sign out from git
    - Open `Keychain Access.app`, delete the Internet password for `github.com`, or
    - `git config --global --unset credential.helper`
1. Push again, and when prompted to enter password, enter a personal access token.
