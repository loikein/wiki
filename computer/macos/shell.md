# Shell

## System Info

Find main board ID:

```bash
$ ioreg -l | grep board-id
```

Find Mac model ID:

```bash
$ sysctl hw.model
```

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

## System Maintenance

Kill Quick Look:

```bash
$ killall -9 -v QuickLookUIService
```

When trackpad is malfunctioning:

```bash
$ killall Dock
```

When `stow` complains about it:

```bash
# Find and delete all .DS_Store files in current folder
$ find . -name '.DS_Store' -type f -delete
```

Show hidden files: \([credit](https://apple.stackexchange.com/a/100040/218914)\)

```bash
$ defaults write com.apple.finder AppleShowAllFiles 1
```

### Danger Zone

When some file cannot be accessed:

```bash
$ sudo chown -R $(whoami) $(brew --prefix)/*
```

Edit host file:

```bash
$ sudo subl /private/etc/hosts
```

## Working With `npm`

```bash
$ npm list -g --depth=0
```

```bash
$ npm -g uninstall <name> --save
```

## Working with LaTeX

When `\xdef\@fontenc@load@list{\@fontenc@load@list undefined control sequence` happens: \([credit](https://stackoverflow.com/a/60493558/10668706)\)

```bash
$ fmtutil-sys --all
```

