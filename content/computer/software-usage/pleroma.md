---
weight: 400
title: "Pleroma"
---

## Installation on Raspberry Pi

Mostly following [Pleroma and Mastodon on the Raspberry Pi 3 · wimvanderbauwhede/limited-systems Wiki](https://github.com/wimvanderbauwhede/limited-systems/wiki/Pleroma-and-Mastodon-on-the-Raspberry-Pi-3).

- Check system compatibility: \([ref](https://docs-develop.pleroma.social/backend/installation/otp_en/#detecting-flavour)\)

    ```bash
    $ arch="$(uname -m)";if [ "$arch" = "x86_64" ];then arch="amd64";elif [ "$arch" = "armv7l" ];then arch="arm";elif [ "$arch" = "aarch64" ];then arch="arm64";else echo "Unsupported arch: $arch">&2;fi;if getconf GNU_LIBC_VERSION>/dev/null;then libc_postfix="";elif [ "$(ldd 2>&1|head -c 9)" = "musl libc" ];then libc_postfix="-musl";elif [ "$(find /lib/libc.musl*|wc -l)" ];then libc_postfix="-musl";else echo "Unsupported libc">&2;fi;echo "$arch$libc_postfix"
    # arm
    ```

- Increase SWAP size:

    ```bash
    $ sudo nano /etc/dphys-swapfile
    # set CONF_SWAPSIZE=256

    $ /etc/init.d/dphys-swapfile restart
    ```

- Set static IP address:

    ```bash
    $ sudo nano /etc/dhcpcd.conf
    # find something like this or add:
    # interface wlan0
    # inform <desired IP address>
    # static routers=<router's IP address>
    # static domain_name_servers=<?>
    ```
