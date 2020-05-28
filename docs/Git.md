## General

```sh
# Difference btw now and last commit
$ git diff HEAD^..HEAD

# Initial pull submodule
$ git submodule update --init --recursive

# Update all submodules
$ git submodule -q foreach git pull -q origin master

# Show remote URL
$ git remote show origin

# Change last commit message
$ git commit --amend

# Show the file tree under git version control
$ git ls-tree --full-tree -r --name-only HEAD

# Gently squash last two commits
# Commit first!!
$ git reset --soft HEAD~2 && git commit --edit -m"$(git log --format=%B --reverse HEAD..HEAD@{1})"
```

## `.gitignore`

```sh
# Add late ignore
$ git commit -m "add/change .gitignore"

$ subl .gitignore

# .DS_Store
# **/.DS_Store

# Apply change
$ git rm -r --cached . && git add . && git commit -m ".gitignore is now working"
```
