---
weight: 400
title: "Automator & AppleScript"
---

For anyone who wants to learn this particular art, please read first:  
[Daring Fireball: The English-Likeness Monster](https://daringfireball.net/2005/09/englishlikeness_monster)

> My OS version is macOS 10.15. Things may have changed in newer versions.
{.book-hint .warning}

## Copy link of file

Type: Quick Action workflow

```applescript
on run {input, parameters}
    set thePath to POSIX path of input
    set the clipboard to "file://" & thePath as text
end run
```

![Copy link of file usage](/img/automator_file_link.png)

<!-- ## Copy as markdown

[Macro to copy safari or chrome selection as markdown - Questions & Suggestions - Keyboard Maestro Discourse](https://forum.keyboardmaestro.com/t/macro-to-copy-safari-or-chrome-selection-as-markdown/9592) -->

## Word count

Type: Service

Ref: [How to Set Up a System-Wide Word Count Service on Your Mac - MacRumors](https://www.macrumors.com/how-to/system-wide-word-count-service-macos/)

```sh
echo "Words: (-w)"
echo $1 | wc -w
echo "Bytes: (-c)"
echo $1 | wc -c
echo "Characters: (zh -m)"
echo $1 | LANG="zh_CN.UTF-8" wc -m
```

![Word count usage](/img/automator_word_count.png)

## Make symlink

Ref: [macos - Quick way to create a symlink? - Ask Different](https://apple.stackexchange.com/questions/357022/quick-way-to-create-a-symlink)
