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

## Configure LCD Display

```bash
$ git clone  https://github.com/goodtft/LCD-show.git
$ chmod -R 755 LCD-show
$ cd LCD-show/
$ sudo ./LCD35-show
```

<!-- 
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

- Reboot: `$ sudo shutdown -r now` or `$ sudo reboot`
- Shutdown: `$ ` or `$ sudo halt`
- See list of running processes by uptime: `$ ps -aux --sort -time`

## Troubleshooting

### Something 1

Try in sequence: `$ sudo apt-get clean`

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

If see this:

```text
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
```

Try this:

```bash
$ ssh-keygen -R "<ip of server>"
```
