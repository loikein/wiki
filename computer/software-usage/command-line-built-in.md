# Built-In Shell Commands

References:

- [The Linux man-pages project](https://www.kernel.org/doc/man-pages/)
- [Data Wrangling · the missing semester of your cs education](https://missing.csail.mit.edu/2020/data-wrangling/)

Benchmark for some of the examples:

```bash
$ curl --head --silent google.com
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

## grep

Online manual: [grep(1) - Linux manual page](https://man7.org/linux/man-pages/man1/grep.1.html)

Example:

```bash
$ curl --head --silent google.com | grep GMT
# Date: Fri, 07 Aug 2020 19:19:53 GMT
# Expires: Sun, 06 Sep 2020 19:19:53 GMT
```

## less

Online manual: [less(1) - Linux manual page](https://man7.org/linux/man-pages/man1/less.1.html)

Text displayer, or: pager.

```bash
$ curl www.google.com | less
```

## sed

Online manual: [sed(1) - Linux manual page](https://man7.org/linux/man-pages/man1/sed.1.html)  
Documentation: [sed, a stream editor](https://www.gnu.org/software/sed/manual/sed.html)

- Non-greedy regex matching: `sed -E 's/regex/replacement/'` (E for regexp-extended)
- Greedy matching: `sed -E 's/regex/replacement/g'`

Example 1:

```bash
$ curl --head --silent google.com | grep GMT | sed -E 's/^.*[A-Za-z]{3}, [0-9]{2} [A-Za-z]{3} 2020 (.*)$/\1/'
# 19:40:05 GMT
# 19:40:05 GMT
```

Example 2: FizzBuzz \([credit](https://rosettacode.org/wiki/FizzBuzz#Sed)\)

```bash
$ seq 15 | sed '/.*[05]$/s//Buzz/; n; s//Buzz/; n; s//Buzz/; s/^[0-9]*/Fizz/'
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

## tac

Online manual: [tac(1) - Linux manual page](https://man7.org/linux/man-pages/man1/tac.1.html)

Display output upside-down, i.e., the reverse of `cat`.

Example 1:

```bash
$ cat README.md
# # Introduction
# 
# My personal wiki, cheat sheet, knowledge base…
# Each page is written in the language in which I think about the topic.
# 
# An experiment inspired by [Nikita Voloboev's Personal Wiki](https://wiki.nikitavoloboev.xyz/).
# 

$ tac README.md
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
$ curl --head --silent google.com | tac
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

## top

Online manual: [top(1) - Linux manual page](https://man7.org/linux/man-pages/man1/top.1.html)

Activity monitor in the shell.
