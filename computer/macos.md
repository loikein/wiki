## System Maintenance

```sh
# Kill Quick Look
$ killall -9 -v QuickLookUIService
```

When trackpad is malfunctioning:

```sh
# Kill dock
$ killall Dock
```

When `stow` complains about it:

```sh
# Find and delete all .DS_Store files in current folder
$ find . -name '.DS_Store' -type f -delete
```

### Danger Zone

When some file cannot be accessed:

```sh
$ sudo chown -R $(whoami) $(brew --prefix)/*
```

## Working With `npm`

```sh
$ npm list -g --depth=0
```

```sh
$ npm -g uninstall <name> --save
```

## Working with LaTeX

When `\xdef\@fontenc@load@list{\@fontenc@load@list undefined control sequence` happens: ([credit](https://stackoverflow.com/a/60493558/10668706))

```sh
$ fmtutil-sys --all
```

