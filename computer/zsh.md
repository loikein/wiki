# Zsh

<!-- TODO: explain my .zshrc line-by-line. -->

## Set Language

Set everything to English:

```text
# In .zshrc

export LANG=en_US.UTF-8
```

…except `git`: \([credit](https://askubuntu.com/a/320663)\)

```text
# In .zshrc

alias git='LANG="zh_CN.UTF-8" git'
```

## Print All Colours

```sh
$  for i in {0..255}; do print -Pn "%K{$i}  %...)i}%f " ${${(M)$((i%6)):#3}:+$'\n'}; done
```

## Antigen

Repository: [zsh-users/antigen: The plugin manager for zsh.](https://github.com/zsh-users/antigen)

Note: The `antigen bundle <<EOBUNDLES EOBUNDLES` thing does not work. Add each plugin line-by-line.
