---
weight: 100
title: "CLI: System & Web"
---

References:

- [The Linux man-pages project](https://www.kernel.org/doc/man-pages/)
- [Data Wrangling · the missing semester of your cs education (2020)](https://missing.csail.mit.edu/2020/data-wrangling/)
- [Command-line environment · the missing semester of your cs education (2019)](https://missing.csail.mit.edu/2019/command-line/)

## buku (browser bookmark manager)

Repository: [jarun/buku: Browser-independent bookmark manager](https://github.com/jarun/buku)

## cd

Online manual: [cd(1p) - Linux manual page](https://man7.org/linux/man-pages/man1/cd.1p.html)

```bash
# Go to home
cd ~

# Go to last directory
cd -
```

## ls

### exa

Repository: [ogham/exa: A modern version of ‘ls’.](https://github.com/ogham/exa)  
Documentation: [Command-line options · exa](https://the.exa.website/docs/command-line-options)

- Modified date in reverse order (newest on top): `exa --long --reverse --sort=modified` or `ll -rs=mod` with alias below.
- Always put folders on top: `exa --group-directories-first`

Useful alias:

```bash
alias ls='exa --all --icons'
alias ll='exa --all --icons --header --long'
alias lt='exa --all --icons --header --long --tree --level=2'
```

## man

### tldr

Repository: [tldr-pages/tldr: 📚 Collaborative cheatsheets for console commands](https://github.com/tldr-pages/tldr)  
Documentation: [tldr pages](https://tldr.sh/)

Example:

```bash
tldr cat
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

## mv

Ref: [Shell Command Language](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html)

Batch change filename: ([credit 1](https://unix.stackexchange.com/a/56812), [2](https://unix.stackexchange.com/questions/19654/how-do-i-change-the-extension-of-multiple-files#comment406782_19656))

```bash
# add text before filename
for f in *; do mv "$f" "something-${f%}"; done

# add text after filename but before extension
for f in *.txt; do mv "$f" "${f%.txt}-something.txt"; done

# change extension
for f in *.txt; do mv "$f" "${f%.txt}.html"; done
```

## ping

### nmap (ping for local devices)

- Ping iPhone: `nmap -Pn <ip address>`

## ranger (file manager)

Repository: [ranger/ranger: A VIM-inspired filemanager for the console](https://github.com/ranger/ranger)  
Documentation: [ranger.github.io/](https://ranger.github.io/)

Add some icons: [alexanderjeurissen/ranger_devicons: Ranger plugin that adds file glyphs / icon support to Ranger](https://github.com/alexanderjeurissen/ranger_devicons)

## top

Online manual: [top(1) - Linux manual page](https://man7.org/linux/man-pages/man1/top.1.html)

Activity monitor in the shell.

- Help: `?`
- Sort by name: `o`
- Search by pid: `O`

### htop

Repository: [hishamhm/htop: htop is an interactive text-mode process viewer for Unix systems. It aims to be a better 'top'.](https://github.com/hishamhm/htop)  
Online manual: [htop(1) - Linux manual page](https://www.man7.org/linux/man-pages/man1/htop.1.html)

