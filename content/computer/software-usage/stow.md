---
weight: 400
title: "stow"
description: "Best dotfile manager ever."
---

If you do not know what is a dotfile, see: [Dotfiles – What is a Dotfile and How to Create it in Mac and Linux](https://www.freecodecamp.org/news/dotfiles-what-is-a-dot-file-and-how-to-create-it-in-mac-and-linux/)

Useful links

- [GitHub does dotfiles - dotfiles.github.io](https://dotfiles.github.io/)
- [mathiasbynens/dotfiles](https://github.com/mathiasbynens/dotfiles)

## Basics

```sh
# if get error do
find . -name '.DS_Store' -type f -delete

# add package
stow <folder>

# remove package (only symlinks, no file is deleted)
stow --delete <folder>
```

## Global ignores

In file `~/dotfiles/.stow-global-ignore`, put stuff like

```sh
\.log
\.git
\.gitignore
```
