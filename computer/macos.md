# macOS

## Hardware

The `delete` on Mac keyboards functions as `backspace`, but `fn` + `delete` function as the actual `del`.

## Software

Programmes that I love or cannot use my Mac without.

### System-Maintenance Related Software

TBA

### Export Safari Reading List

According to [Export a list of URLs from Safari Reading List – alexwlchan](https://alexwlchan.net/2015/11/export-urls-from-safari-reading-list/), just download the script and put it anywhere, then call it with `python3 readinglist.py`.

Just in case, I have created a copy of the script [here](https://gist.github.com/loikein/d9ebc90e65839c81088ec65caca3ebbe).

### Parallels Desktop

```text
devices.mac_hw_model = "MacBookPro15,2"
devices.smbios.board_id = "Mac-827FB448E656EC26"
```

## App Store

### Get App Bundle ID

Reference: [Finding the App Bundle ID | PSPDFKit](https://pspdfkit.com/guides/ios/current/faq/finding-the-app-bundle-id/)

1. With a store link, copy the app ID, and access the URL: `https://itunes.apple.com/lookup?id=ID`.
1. If everything has been typed correctly, the URL will return a `.txt` file.
1. Open the file, among the last lines (the 4th last for now) is a name `bundleID`.
1. The corresponding value is the bundle ID of this app.

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

### System Setting & Maintenance

Check SIP status:

```bash
$ csrutil status
# System Integrity Protection status: enabled.
```

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

### Danger Zone

Reference: [How to remove driver and kexts on Mac? : SteamController](https://www.reddit.com/r/SteamController/comments/edkq1r/how_to_remove_driver_and_kexts_on_mac/)

When some file cannot be accessed:

```bash
$ sudo chown -R $(whoami) $(brew --prefix)/*
```

Edit host file:

```bash
$ sudo subl /private/etc/hosts
```
