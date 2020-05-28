## General

```sh
# Difference btw now and last commit
$ git diff HEAD^..HEAD
```

```sh
# Initial pull submodule
$ git submodule update --init --recursive
```

```sh
# Update all submodules
$ git submodule -q foreach git pull -q origin master
```

```sh
# Show remote URL
$ git remote show origin
```

```sh
# Change last commit message
$ git commit --amend
```

```sh
# Show the file tree under git version control
$ git ls-tree --full-tree -r --name-only HEAD
```

```sh
# Gently squash last two commits
# Commit first!!
$ git reset --soft HEAD~2 && git commit --edit -m"$(git log --format=%B --reverse HEAD..HEAD@{1})"
```

## `.gitignore`

```sh
# Add late ignore
$ git commit -m "add/change .gitignore"
$ subl .gitignore
```

In `.gitignore`:

```
.DS_Store
**/.DS_Store
```


```sh
# Apply change
$ git rm -r --cached . && git add . && git commit -m ".gitignore is now working"
```
