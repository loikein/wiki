# Other macOS Software

Programmes that I love or cannot use my Mac without. 

Also see [macOS Maintenance \#Useful Software](../system-maintenance/macos.md#useful-software).

## Safari

### Access Tabs/Reading List w/o Opening Safari

[josh-/CloudyTabs: CloudyTabs is a simple menu bar application that lists your iCloud Tabs.](https://github.com/josh-/CloudyTabs)

### Export Safari Reading List

According to [Export a list of URLs from Safari Reading List – alexwlchan](https://alexwlchan.net/2015/11/export-urls-from-safari-reading-list/), just download the script and put it anywhere, then call it with `python3 readinglist.py`.

Just in case, I have created a copy of the script [here](https://gist.github.com/loikein/d9ebc90e65839c81088ec65caca3ebbe).

## App Store

### Get App Bundle ID

Reference: [Finding the App Bundle ID \| PSPDFKit](https://pspdfkit.com/guides/ios/current/faq/finding-the-app-bundle-id/)

1. With a store link, copy the app ID, and access the URL: `https://itunes.apple.com/lookup?id=ID`.
1. If everything has been typed correctly, the URL will return a `.txt` file.
1. Open the file, among the last lines (the 4th last for now) is a name `bundleID`.
1. The corresponding value is the bundle ID of this app.

## Parallels Desktop

To run macOS 10.16 Big Sur on Parallels, enter flags in setting:

```text
devices.mac_hw_model = "MacBookPro15,2"
devices.smbios.board_id = "Mac-827FB448E656EC26"
```
