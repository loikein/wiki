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
