# Git

## General

```bash
# Difference btw now and last commit
$ git diff HEAD^..HEAD
```

```bash
# Show remote URL
$ git remote show origin
```

```bash
# Change last commit message
$ git commit --amend
```

```bash
# Show the file tree under git version control
$ git ls-tree --full-tree -r --name-only HEAD
```

```bash
# Gently squash last two commits
# Commit first!!
$ git reset --soft HEAD~2 && git commit --edit -m"$(git log --format=%B --reverse HEAD..HEAD@{1})"
```

## `.gitignore`

```bash
# Add late ignore
$ git commit -m "add/change .gitignore"
$ subl .gitignore
```

In `.gitignore`:

```text
.DS_Store
**/.DS_Store
```

```bash
# Apply change
$ git rm -r --cached . && git add . && git commit -m ".gitignore is now working"
```

## Submodules

[Easy way to pull latest of all git submodules - Stack Overflow](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules)

```bash
# Initial pull submodule
$ git submodule update --init --recursive
```

```bash
# Update all submodules
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

