---
weight: 400
title: "Shimeji for Mac"
---

# Shimeji for Mac

Main reference: [@zkdlsoo on Twitter](https://twitter.com/zkdlsoo/status/986176637946359808)

This article was originally posted in Chinese on my blog: [Shimeji（桌宠） on macOS](https://blog.loikein.one/posts/2021-02-22-shimeji-for-macos/). Go take a look at my demo video there if you want to know how it looks in action.

## Prerequisites

1. A relatively high-spec Mac. This thing eats a lot of CPU.
1. Java 6 runtime
    - Can be downloaded from [Apple's kb](https://support.apple.com/kb/DL1572?locale=en_US).
    - Or use Homebrew: `$ brew install java6`
1. The Shimeji (for Windows) of your choice
1. One working Shimeji for Mac
    - Download either `2P!England (single)` or `2P!America (single)` from [-Mac- 2PUS and 2PUK -Mac- Shimeji by lalala00000007 on DeviantArt](https://www.deviantart.com/lalala00000007/art/Mac-2PUS-and-2PUK-Mac-Shimeji-360524267).
    - Note that those two files have different passwords.
    - Oh, my, is it Hetalia? It is indeed Hetalia.
    - I am terribly sorry for abusing your work, dear author, but it is the one and only working example on Earth now.

## Installation

1. Unzip the Shimeji of your choice to, say, `folder1`.
1. Unzip the Hetalia Shimeji to `folder2`.
1. Just to make sure, try running it first.
    a. Right click `folder2/Shimeji.app`, and click `Show Package Contents`.
    b. Find `Shimeji.app/Contents/Resources/Java/Shimeji.jar`, double click to run.
    c. Does it work? It worked on my machine (macOS 10.15).
    d. To make it easier to access, make a symlink. Right click `Shimeji.jar`, and click `Make Alias`. Now cut & paste this directly under `folder2`.
1. Rename `folder2/img/` to something else, say, `img_2`.
1. Copy `folder1/img/` & paste under `folder2/`.
1. Observe the structure of `folder2/img_2/`. This is the target structure.
    - It contains one `icon.png` and several `shimeXX.png`.
    - Everything is put directly under the folder, no subfolders.
1. Observe the structure of `folder2/img/`. If it is different to `folder2/img_2/`, edit accordingly.
1. Run `Shimeji.jar` again. This time the Shimeji of your choice should show up.

## Translation of the menu items

From top to bottom:

- Add one more
- Gather all
- Clean all but one
- Restore window (no idea what this does)
- Exit
