---
title: "macOS"
---
## Readings

- [Mac Shortcuts: Aliases, Symbolic Links, Hard Links](https://www.lifewire.com/aliases-symbolic-links-hard-links-mac-2260189)


## Useful Software

### Setting

- [Titanium Software \| Operating system utilities for Mac \- OnyX](https://www.titanium-software.fr/en/onyx.html)
- [TinkerTool: Description](https://www.bresink.com/osx/TinkerTool.html)

### Runtime/Internet

- [App Tamer](https://www.stclairsoft.com/AppTamer/)
- [Objective-See: KnockKnock](https://objective-see.com/products/knockknock.html)
- [Objective-See: LuLu](https://objective-see.com/products/lulu.html)

### Microphone/Camera

- [Objective-See: OverSight](https://objective-see.com/products/oversight.html)

## Printer

### Hold for Authentication

In Keychain Access.app, search for name of the printer, delete the password, and try again.

The `sudo lpadmin -p [printer-name] -o auth-info-required=username,password` command suggested on [this website](https://www.papercut.com/kb/Main/HoldforAuthentication/) does not work although it looks like it should.


## Shell

### System Info

Find main board ID:

```sh
ioreg -l | grep board-id
```

Find Mac model ID:

```sh
sysctl hw.model
```

Find MAC address:

```sh
ifconfig en0 | grep ether
```

### Allow app downloads from anywhere

Credit: [How to allow apps downloaded from anywhere on Mac](https://macpaw.com/how-to/allow-apps-anywhere)

```sh
sudo spctl --master-disable
```

### Solve "App is damaged and can't be opened"

Credit: [macOS Catalina: "App is damaged and can't be opened. You should move it to the trash." - Ask Different](https://apple.stackexchange.com/a/372208)

```sh
sudo xattr -rd com.apple.quarantine "path/to/file.app"
```

### Useful Operations

Restart Quick Look:

```sh
killall -9 -v QuickLookUIService
```

Restart Touch Bar:

```sh
pkill "Touch Bar agent"; killall "ControlStrip"
```

Restart paste board:

```sh
killall pboard
```

When trackpad is malfunctioning:

```sh
killall Dock
```

Find and delete all .DS_Store files in current folder: \([credit](https://jonbellah.com/articles/recursively-remove-ds-store)\)

```sh
find . -name '.DS_Store' -type f -delete
```

Fix Xcode hanging in Terminal: \([credit](https://apple.stackexchange.com/a/308125)\)

```sh
sudo xcodebuild -license accept
```

Restart bluetooth service: (requires [blueutil](https://github.com/toy/blueutil), [credit](https://apple.stackexchange.com/a/310732))

```sh
blueutil -p 0 && sleep 1 && blueutil -p 1
```

<!-- Stop spaces auto switching \(auto-swoosh\): \(credits: [1](https://apple.stackexchange.com/a/4821), [2](https://apple.stackexchange.com/a/423294)\)

```bash
defaults write com.apple.Dock workspaces-auto-swoosh -bool YES && killall Dock

defaults write -g AppleSpacesSwitchOnActivate -bool YES && killall Dock
``` -->

### Advanced Settings

Check SIP status:

```sh
csrutil status
# System Integrity Protection status: enabled.
```

Enable three-finger dragging: \([credit](https://apple.stackexchange.com/a/362308)\)

```sh
defaults write com.apple.AppleMultitouchTrackpad TrackpadThreeFingerDrag 1 && defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadThreeFingerDrag 1
```

Show hidden files: \([credit](https://apple.stackexchange.com/a/100040/218914)\)

```sh
defaults write com.apple.finder AppleShowAllFiles 1
```

Turn off Power Chime: \([credit](https://apple.stackexchange.com/a/309947)\)

```sh
defaults write com.apple.PowerChime ChimeOnNoHardware 0
killall PowerChime
```

Make hidden apps' icon transparent in the dock: \([credit](https://missing.csail.mit.edu/2019/os-customization/#macos)\)

```sh
defaults write com.apple.dock showhidden 1
killall Dock
```

Show Safari develop & debug menu item: \([credit](https://oku.edu.mie-u.ac.jp/~okumura/macosx/)\)

```sh
defaults write com.apple.Safari IncludeDebugMenu 1
defaults write com.apple.Safari IncludeInternalDebugMenu 1
```

Disable elastic scrolling in Safari: \([credit](https://osxdaily.com/2012/05/10/disable-elastic-rubber-band-scrolling-in-mac-os-x/)\)

```sh
defaults write -g NSScrollViewRubberbanding 0
```

### Find Third Party Kernel Extensions

[Credit](https://apple.stackexchange.com/a/310758)

```sh
kextstat | grep -v com.apple
```

## Danger Zone

### Remove Snapz Pro

[Credit](https://www.macworld.com/article/3128854/how-to-remove-snapz-pro-in-macos-sierra.html)

```sh
sudo kextunload -b com.AmbrosiaSW.AudioSupport

cd /Library/Extensions/
sudo rm -r AmbrosiaAudioSupport.kext # r for recursive

cd /Library/LaunchDaemons/
sudo rm com.ambrosiasw.ambrosiaaudiosupporthelper.daemon.plist

cd ~/Library/Containers/
sudo rm -r com.ambrosiasw.snapz-pro-x
```

### Edit Launch Items

\([credit 1](https://stackoverflow.com/a/16727754), [2](https://apple.stackexchange.com/a/308421)\)

- PID: running
- Status:
    - `0` = finished
    - Positive = error
    - Negative = terminated

```sh
# Find
launchctl list | grep epicgames
# PID     Status  Label
# -       1       com.epicgames.launcher

# Remove
launchctl remove com.epicgames.launcher
```

### Edit File Status

Reference: [How to remove driver and kexts on Mac? : SteamController](https://www.reddit.com/r/SteamController/comments/edkq1r/how_to_remove_driver_and_kexts_on_mac/)

When some file cannot be accessed by Homebrew:

```sh
sudo chown -R $(whoami) $(brew --prefix)/*
```

### Edit Host File

```sh
sudo subl /private/etc/hosts
```
