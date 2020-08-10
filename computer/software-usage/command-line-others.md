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

## Others

### buku (bookmark manager)

Repository: [jarun/buku: Browser-independent bookmark manager](https://github.com/jarun/buku)

### fzf (find anything)

Repository: [junegunn/fzf: A command-line fuzzy finder](https://github.com/junegunn/fzf)  
A great demo video: [Vim universe. fzf - command line fuzzy finder - YouTube](https://www.youtube.com/watch?v=qgG5Jhi_Els)

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
