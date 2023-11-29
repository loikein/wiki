---
weight: 400
title: "Homebrew"
---

## Useful commands

### List dependencies of a package

Ref: [dependency management - Easy way to have Homebrew list all package dependencies - Stack Overflow](https://stackoverflow.com/a/52120368)

```sh
brew deps --tree --installed vim
```

### List all installed packages and dependencies

\(Might be out of date, haven't checked for a while\)

Ref: [Homebrew: List packages and what uses them | Thingy Ma jig](https://www.thingy-ma-jig.co.uk/blog/22-09-2014/homebrew-list-packages-andw-what-uses-them)

```sh
# takes a long time to run and the output is very long
brew list -1 | while read cask; do echo -ne "\x1B[1;34m $cask \x1B[0m"; brew uses $cask --installed | awk '{printf(" %s ", $0)}'; echo ""; done
```

## Debugging

<!--
### Using Homebrew with unsupported macOS version

Good to have installed:

- cmake \(because everything is make-installed\)
- curl
- rust
- sqlite
- qt \(for pip, see [python - Error while installing pytq5 with pip: Preparing metadata (pyproject.toml) did not run successfully - Stack Overflow](https://stackoverflow.com/a/71669996)\)
-->

### Edit formula

Ref: [compilation - How do I modify a Homebrew formula? - Stack Overflow](https://stackoverflow.com/a/75520170)

```sh
brew rm <formula>
brew edit <formula>
export HOMEBREW_NO_INSTALL_FROM_API=1
brew reinstall --build-from-source <formula>

brew pin <formula>
```

### `FormulaUnavailableError: No available formula with the name...`

```sh
brew update
brew tap homebrew/core
# takes a long time to run, depending on internet speed
```

### `Error: Could not symlink...`

[Homebrew: Could not symlink, /usr/local/bin is not writable - Stack Overflow](https://stackoverflow.com/a/26647594)

```sh
sudo chown -R `whoami`:admin ...
```

<!-- 
### Python 3.12 installation

`install: Modules/_tkinter.cpython-312-darwin.so: No such file or directory`: \([ref](https://stackoverflow.com/a/67465708)\)

[Why does Python installed via Homebrew not include Tkinter - Stack Overflow](https://stackoverflow.com/a/59763871)
→
[MacOS homebrew python 3.8.6 with tcl-tk (properly)](https://gist.github.com/iexa/2ac761bfd96ab78988b76c030d54a5b8)

```sh
brew install python-tk
```

 -->

## Brewfile

Blog post: [Mac 重装清单](https://blog.loikein.one/posts/2020-01-05-mac-restore-list/)

Generate
: `brew bundle dump --describe`

Recover
: `brew bundle --file="~/Brewfile"`

{{< gist
gist="57bbda0722a5b2aee5d5f2f616fc6194"
file="Brewfile"
lang="sh" >}}
