# macOS Maintenance

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

## Shell

### System Info

Find main board ID:

```bash
$ ioreg -l | grep board-id
```

Find Mac model ID:

```bash
$ sysctl hw.model
```

### Useful Operations

Kill Quick Look:

```bash
$ killall -9 -v QuickLookUIService
```

When trackpad is malfunctioning:

```bash
$ killall Dock
```

Find and delete all .DS_Store files in current folder:

```bash
$ find . -name '.DS_Store' -type f -delete
```

Fix Xcode hanging: \([credit](https://apple.stackexchange.com/questions/119864/xcodebuild-firing-after-every-terminal-command)\)

```bash
$ sudo xcodebuild -license accept
```

### Settings

Check SIP status:

```bash
$ csrutil status
# System Integrity Protection status: enabled.
```

Enable three-finger dragging: \([credit](https://apple.stackexchange.com/a/362308)\)

```bash
$ defaults write com.apple.AppleMultitouchTrackpad TrackpadThreeFingerDrag 1 && defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadThreeFingerDrag 1
```

Show hidden files: \([credit](https://apple.stackexchange.com/a/100040/218914)\)

```bash
$ defaults write com.apple.finder AppleShowAllFiles 1
```

Turn off Power Chime: \([credit](https://apple.stackexchange.com/a/309947)\)

```bash
$ defaults write com.apple.PowerChime ChimeOnNoHardware 0
$ killall PowerChime
```

Make hidden apps' icon transparent in the dock: \([credit](https://missing.csail.mit.edu/2019/os-customization/#macos)\)

```bash
$ defaults write com.apple.dock showhidden 1
$ killall Dock
```

Show Safari develop & debug menu item: \([credit](https://oku.edu.mie-u.ac.jp/~okumura/macosx/)\)

```bash
$ defaults write com.apple.Safari IncludeDebugMenu 1
$ defaults write com.apple.Safari IncludeInternalDebugMenu 1
```

### Find Third Party Kernel Extensions

[Credit](https://apple.stackexchange.com/a/310758)

```bash
$ kextstat | grep -v com.apple
```

## Danger Zone

### Remove Snapz Pro

[Credit](https://www.macworld.com/article/3128854/how-to-remove-snapz-pro-in-macos-sierra.html)

```bash
$ sudo kextunload -b com.AmbrosiaSW.AudioSupport

$ cd /Library/Extensions/
$ sudo rm -r AmbrosiaAudioSupport.kext # r for recursive

$ cd /Library/LaunchDaemons/
$ sudo rm com.ambrosiasw.ambrosiaaudiosupporthelper.daemon.plist

$ cd ~/Library/Containers/
$ sudo rm -r com.ambrosiasw.snapz-pro-x
```

### Edit Launch Items

\([credit 1](https://stackoverflow.com/a/16727754), [2](https://apple.stackexchange.com/a/308421)\)

- PID: running
- Status:
    - `0` = finished
    - Positive = error
    - Negative = terminated

```bash
# Find
$ launchctl list | grep epicgames
# PID     Status  Label
# -       1       com.epicgames.launcher

# Remove
$ launchctl remove com.epicgames.launcher
```

### Edit File Status

Reference: [How to remove driver and kexts on Mac? : SteamController](https://www.reddit.com/r/SteamController/comments/edkq1r/how_to_remove_driver_and_kexts_on_mac/)

When some file cannot be accessed by Homebrew:

```bash
$ sudo chown -R $(whoami) $(brew --prefix)/*
```

### Edit Host File

```bash
$ sudo subl /private/etc/hosts
```
