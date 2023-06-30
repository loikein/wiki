---
weight: 20
title: "Zsh"
---

<!-- TODO: explain my .zshrc line-by-line. -->

My notes on Unix/shell basics from ages ago \(in Chinese\): [notes: bash](https://gist.github.com/loikein/f7f1e470426c685a1c920c4b944e6c55)

## Set Language

Set everything to English:

```sh
# In .zshrc
export LANG=en_US.UTF-8
```

…except `git`: \([credit](https://askubuntu.com/a/320663)\)

```sh
# In .zshrc
alias git='LANG="zh_CN.UTF-8" git'
```

## Custom motd (message of the day)

Blog post: [macOS + zsh 上使用 Neofetch 作为欢迎语（MotD）](https://blog.loikein.one/posts/2020-03-25-use-neofetch-as-motd-on-mac/)

In shell:

```sh
brew install macchina
cd ~
touch motd.sh
```

In `~/motd.sh`:

```sh
#! /usr/bin/env zsh
macchina --theme Helium
```

In `~/.zshrc`:

```sh
# display motd
if [[ -e $HOME/motd.sh ]]; then source $HOME/motd.sh; fi
```

## Print All Colours

```sh
for i in {0..255}; do print -Pn "%K{$i}  %k%F{$i}${(l:3::0:)i}%f " ${${(M)$((i%6)):#3}:+$'\n'}; done

# or

for i in {0..255}; do printf "\x1b[38;5;${i}mcolour${i}\x1b[0m\n"; done
```

## Antigen

Repository: [zsh-users/antigen: The plugin manager for zsh.](https://github.com/zsh-users/antigen)

Note: The `antigen bundle <<EOBUNDLES EOBUNDLES` thing does not work. Add each plugin line-by-line.
