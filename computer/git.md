# Git

## General

Difference between most recent commit and second most recent commit:

```bash
$ git diff HEAD^..HEAD
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
$ git reset --soft HEAD~2 && git commit --edit -m"$(git log --format=%B --reverse HEAD..HEAD@{1})"
```

## `.gitignore`

Add late ignore:

```bash
$ git commit -m "add/change .gitignore"
$ subl .gitignore
```

In `.gitignore`:

```text
.DS_Store
**/.DS_Store
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

Ref: [Easy way to pull latest of all git submodules - Stack Overflow](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules)

Initial pull submodule:

```bash
$ git submodule update --init --recursive
```

Update all submodules:

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

