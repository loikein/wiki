---
title: "Raspberry Pi"
---

## Fresh Install

1. Install `raspberry-pi-imager` on macOS.
1. Plug in a microSD card, and flash Raspberry Pi OS.
1. Add a file called `ssh` (no extension, no contents) to the top folder.
1. Add a file called `wpa_supplicant.conf` with:

    ```text
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    country=DE

    network={
        ssid="wifi-name"
        psk="password"
        key_mgmt=WPA-PSK
    }
    ```

1. Plug the microSD to Raspberry Pi, connect to power cable.
1. Run ssh to the Pi with `ssh pi@192.168.0.105` (the IP address may differ).
    - The initial password is `raspberry`.
    - The pre-install text editor is `nano`.

When connected to a screen, Pi will prompt to upgrade stuff. Don't do it (press `skip`).

## Use VNC Environment for Remote Desktop

Reference: [How to Use IOS Devices As a Monitor of Raspberry Pi : 6 Steps (with Pictures) - Instructables](https://www.instructables.com/How-to-Use-Ios-Devices-As-a-Monitor-of-Raspberry-P/)

- SSH to the Pi.
- Run `$ sudo apt-get install tightvncserver`
- Run `$ tightvncserver`
- Note down the port (`1` for example)
- On a machine with screen, connect to the server (`192.168.0.105:1` for example)

For auto-start at booting, add the following to `$ nano ~/.bashrc`

```bash
if [ -x "$(command -v tightvncserver)" ]; then tightvncserver; fi
```

Do the stuff from iPad:

- iOS SSH client: [‎Termius - SSH client on the App Store](https://apps.apple.com/us/app/termius-ssh-client/id549039908#?platform=ipad)
- iOS VNC client is [‎VNC Viewer - Remote Desktop on the App Store](https://apps.apple.com/us/app/vnc-viewer-remote-desktop/id352019548#?platform=ipad)

<!-- 
## Configure LCD Display

Setup:

```bash
$ git clone  https://github.com/goodtft/LCD-show.git
$ chmod -R 755 LCD-show
$ cd LCD-show/
$ sudo ./LCD35-show
```

Error message:

```bash
ubuntu@ubuntu:~/LCD-show-ubuntu$ sudo ./LCD35-show
cp: cannot create regular file '/usr/share/X11/xorg.conf.d/99-fbturbo.conf': No such file or directory
need to update touch configuration
E: Could not get lock /var/lib/dpkg/lock-frontend. It is held by process 2327 (unattended-upgr)
N: Be aware that removing the lock file is not a solution and may break your system.
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?
cp: cannot stat '/usr/share/X11/xorg.conf.d/10-evdev.conf': No such file or directory
reboot now
```
 -->

## How To…

- See OS info: `$ cat /etc/os-release`
- Reboot: `$ sudo reboot`
- Shutdown: `$ sudo halt`
- See list of running processes by uptime: `$ ps -aux --sort -time`
- SSH without a password:

    ```sh
    $ ssh-copy-id pi@192.168.0.105
    # Number of key(s) added:        1

    # Now try logging into the machine, with:   "ssh 'pi@192.168.0.105'"
    # and check to make sure that only the key(s) you wanted were added.
    $ ssh pi@192.168.0.105
    ```

## Troubleshooting

### `reason is APT is installing or removing packages`

Try in sequence:

```bash
$ sudo apt-get clean

# if that returned error
$ sudo killall apt-get
$ sudo rm /var/lib/apt/lists/lock
$ sudo rm /var/cache/apt/archives/lock
$ sudo rm /var/lib/dpkg/lock
$ sudo apt-get clean
```

### Something 2

```bash
$ sudo rm /var/lib/dpkg/lock
$ sudo dpkg --configure -a
```

### Cannot SSH after re-installation

If see this on local machine:

```text
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
```

Try this:

```bash
$ ssh-keygen -R "<ip of server>" # 192.168.0.105, for example
```
