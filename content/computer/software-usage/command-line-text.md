---
weight: 100
title: "CLI: File & Text"
---

Benchmark for some of the examples:

```bash
curl --head --silent google.com
# HTTP/1.1 301 Moved Permanently
# Location: http://www.google.com/
# Content-Type: text/html; charset=UTF-8
# Date: Fri, 07 Aug 2020 18:26:00 GMT
# Expires: Sun, 06 Sep 2020 18:26:00 GMT
# Cache-Control: public, max-age=2592000
# Server: gws
# Content-Length: 219
# X-XSS-Protection: 0
# X-Frame-Options: SAMEORIGIN
# 
```

## fzf (find files)

Repository: [junegunn/fzf: A command-line fuzzy finder](https://github.com/junegunn/fzf)  
A great demo video: [Vim universe. fzf - command line fuzzy finder - YouTube](https://www.youtube.com/watch?v=qgG5Jhi_Els)

[\[Question\] how can I toggle exact match behavior in fzf · Issue \#1265 · junegunn/fzf](https://github.com/junegunn/fzf/issues/1265)

## grep

Online manual: [grep(1) - Linux manual page](https://man7.org/linux/man-pages/man1/grep.1.html)

- Use extended regex: `grep -E` or `egrep` (E for `extended-regexp`)
- Use fixed string instead of regex: `grep -F` or `fgrep` (F for `fixed-strings`)
- Reverse match (match without): `grep -v` (v for `invert-match`)

Example:

```bash
curl --head --silent google.com | grep GMT
# Date: Fri, 07 Aug 2020 19:19:53 GMT
# Expires: Sun, 06 Sep 2020 19:19:53 GMT
```

### ripgrep, rg

Repository: [BurntSushi/ripgrep: ripgrep recursively searches directories for a regex pattern](https://github.com/BurntSushi/ripgrep)  
Guide: [ripgrep/GUIDE.md at master · BurntSushi/ripgrep](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md)

- Literal match: `rg -F <string>` (F for fixed-strings)
- Case insensitive: `rg -i` (i for ignore-case)

Example: find text in all files in current directory

```sh
rg -i readme
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

## head, tail

Online manual:

- [head(1) - Linux manual page](https://man7.org/linux/man-pages/man1/head.1.html)
- [tail(1) - Linux manual page](https://man7.org/linux/man-pages/man1/tail.1.html)

- By number of lines: `head -n 10 <file name>`, `tail -n 10 <file name>`

Example:

```bash
curl --head --silent google.com | head -n 2
# HTTP/1.1 301 Moved Permanently
# Location: http://www.google.com/

curl --head --silent google.com | tail -n 2
# X-Frame-Options: SAMEORIGIN
# 
```

## less (man, git diff, git log, etc.)

Online manual: [less(1) - Linux manual page](https://man7.org/linux/man-pages/man1/less.1.html)

Text displayer, aka, pager.

```bash
curl www.google.com | less
```

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

curl www.google.com | less
curl www.google.com | bat
```


## sed

Online manual: [sed(1) - Linux manual page](https://man7.org/linux/man-pages/man1/sed.1.html)  
Documentation: [sed, a stream editor](https://www.gnu.org/software/sed/manual/sed.html)

- Non-greedy regex matching: `sed -E 's/regex/replacement/'` (E for regexp-extended)
- Greedy matching: `sed -E 's/regex/replacement/g'`

Example 1:

```bash
curl --head --silent google.com | grep GMT | sed -E 's/^.*[A-Za-z]{3}, [0-9]{2} [A-Za-z]{3} 2020 (.*)$/\1/'
# 19:40:05 GMT
# 19:40:05 GMT
```

Example 2: FizzBuzz \([credit](https://rosettacode.org/wiki/FizzBuzz#Sed)\)

```bash
seq 15 | sed '/.*[05]$/s//Buzz/; n; s//Buzz/; n; s//Buzz/; s/^[0-9]*/Fizz/'
# 1
# 2
# Fizz
# 4
# Buzz
# Fizz
# 7
# 8
# Fizz
# Buzz
# 11
# Fizz
# 13
# 14
# FizzBuzz
```

## sort

Online manual: [sort(1) - Linux manual page](https://man7.org/linux/man-pages/man1/sort.1.html)

- Ascending order: (A-Z): `sort`
- Descending order (Z-A): `sort -r` (r for reverse)
- Ascending number order (1-9): `sort -n` (n for numeric-sort)
- Descending number order (9-1): `sort -nr`

## tac

Online manual: [tac(1) - Linux manual page](https://man7.org/linux/man-pages/man1/tac.1.html)

Display output upside-down, i.e., the reverse of `cat`.

Example 1:

```bash
cat README.md
# # Introduction
# 
# My personal wiki, cheat sheet, knowledge base…
# Each page is written in the language in which I think about the topic.
# 
# An experiment inspired by [Nikita Voloboev's Personal Wiki](https://wiki.nikitavoloboev.xyz/).
# 

tac README.md
# 
# An experiment inspired by [Nikita Voloboev's Personal Wiki](https://wiki.nikitavoloboev.xyz/).
# 
# Each page is written in the language in which I think about the topic.
# My personal wiki, cheat sheet, knowledge base…
# 
# # Introduction
```

Example 2:

```bash
curl --head --silent google.com | tac
# 
# X-Frame-Options: SAMEORIGIN
# X-XSS-Protection: 0
# Content-Length: 219
# Server: gws
# Cache-Control: public, max-age=2592000
# Expires: Sun, 06 Sep 2020 18:26:04 GMT
# Date: Fri, 07 Aug 2020 18:26:04 GMT
# Content-Type: text/html; charset=UTF-8
# Location: http://www.google.com/
# HTTP/1.1 301 Moved Permanently
```

## uniq

Online manual: [uniq(1) - Linux manual page](https://man7.org/linux/man-pages/man1/uniq.1.html)

- Display number of occurrences of each line, sorted by the most frequent: `sort <file> | uniq -c | sort -nr` (c for count, n for number, r for reverse)

## wc

Online manual: [wc(1) - Linux manual page](https://man7.org/linux/man-pages/man1/wc.1.html)

Count number of lines/words/characters.

Example:

```bash
curl --head --silent google.com | wc --lines
curl --head --silent google.com | wc -l
#       11
```
