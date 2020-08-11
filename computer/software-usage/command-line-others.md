# Other Command Line Tools

## Replacement for Built-In Commands

### bat (cat, less)

Repository: [sharkdp/bat: A cat(1) clone with wings.](https://github.com/sharkdp/bat)

- Show non-printable characters: `bat -A` (A for show-all)

Change theme: (in `~/.zshrc`)

```bash
export BAT_THEME='ansi-dark'
```

Example:

```bash
# Compare the outcomes:

$ curl www.google.com | less
$ curl www.google.com | bat
```

### exa (ls)

Repository: [ogham/exa: A modern version of ‘ls’.](https://github.com/ogham/exa)  
Documentation: [Introduction · exa](https://the.exa.website/introduction)

Useful alias:

```bash
alias ls='exa --icons --all'
alias ll='exa --long --icons --all'
alias lt='exa --long --icons --all --tree --level=2'
```

### htop (top)

Repository: [hishamhm/htop: htop is an interactive text-mode process viewer for Unix systems. It aims to be a better 'top'.](https://github.com/hishamhm/htop)  
Online manual: [htop(1) - Linux manual page](https://www.man7.org/linux/man-pages/man1/htop.1.html)

### ripgrep, rg (grep)

Repository: [BurntSushi/ripgrep: ripgrep recursively searches directories for a regex pattern](https://github.com/BurntSushi/ripgrep)  
Guide: [ripgrep/GUIDE.md at master · BurntSushi/ripgrep](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md)

- Literal match: `rg -F <string>` (F for fixed-strings)
- Case insensitive: `rg -i` (i for ignore-case)

Example: find text in all files in current directory

```sh
$ rg -i readme
# programming/static-site/gatsby.md
# 73:    ├── README.md
# 
# computer/software-usage/command-line-built-in.md
# 139:$ cat README.md
# 148:$ tac README.md
# 
# computer/software-usage/command-line-others.md
# 55:$ rg -i readme
# 57:# 139:$ cat README.md
# 58:# 148:$ tac README.md
# 61:# 3:* [Introduction](README.md)
# 62:# 32:* [Python](programming/python/README.md)
# 63:# 56:* [衣着打扮](life-log/dressing-grooming/README.md)
# 64:# 65:* [Entertainment](life-log/entertainment/README.md)
# 67:# 73:    ├── README.md
# 
# SUMMARY.md
# 3:* [Introduction](README.md)
# 32:* [Python](programming/python/README.md)
# 56:* [衣着打扮](life-log/dressing-grooming/README.md)
# 65:* [Entertainment](life-log/entertainment/README.md)
```

## Others

### buku (bookmark manager)

Repository: [jarun/buku: Browser-independent bookmark manager](https://github.com/jarun/buku)

### fzf (find anything)

Repository: [junegunn/fzf: A command-line fuzzy finder](https://github.com/junegunn/fzf)  
A great demo video: [Vim universe. fzf - command line fuzzy finder - YouTube](https://www.youtube.com/watch?v=qgG5Jhi_Els)

### ranger (file manager)

Repository: [ranger/ranger: A VIM-inspired filemanager for the console](https://github.com/ranger/ranger)  
Documentation: [ranger.github.io/](https://ranger.github.io/)

Add some icons: [alexanderjeurissen/ranger_devicons: Ranger plugin that adds file glyphs / icon support to Ranger](https://github.com/alexanderjeurissen/ranger_devicons)

### tldr (simplified man)

Repository: [tldr-pages/tldr: 📚 Collaborative cheatsheets for console commands](https://github.com/tldr-pages/tldr)  
Documentation: [tldr pages](https://tldr.sh/)

Example:

```bash
$ tldr cat
# 
# cat
# 
# Print and concatenate files.
# 
# - Print the contents of a file to the standard output:
#     cat file
# 
# - Concatenate several files into the target file:
#     cat file1 file2 > target_file
# 
# - Append several files into the target file:
#     cat file1 file2 >> target_file
# 
# - Number all output lines:
#     cat -n file
# 
# - Display non-printable and whitespace characters (with `M-` prefix if non-ASCII):
#     cat -v -t -e file
```
