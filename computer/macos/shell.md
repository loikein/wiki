# Shell

## System Maintenance

```bash
# Kill Quick Look
$ killall -9 -v QuickLookUIService
```

When trackpad is malfunctioning:

```bash
# Kill dock
$ killall Dock
```

When `stow` complains about it:

```bash
# Find and delete all .DS_Store files in current folder
$ find . -name '.DS_Store' -type f -delete
```

### Danger Zone

When some file cannot be accessed:

```bash
$ sudo chown -R $(whoami) $(brew --prefix)/*
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

