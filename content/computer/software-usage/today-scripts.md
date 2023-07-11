---
weight: 400
title: "Today-Scripts"
---

{{< hint danger >}}
This programme stopped working after upgrading to macOS 10.12 (Sierra). I collect these scripts here only for future reference purpose.
{{< /hint >}}

Refs:

- [lsd/Today-Scripts: A widget for running scripts in the Today View in OS X Yosemite's Notification Center](https://github.com/lsd/Today-Scripts)
- [Home · SamRothCA/Today\-Scripts Wiki](https://github.com/SamRothCA/Today-Scripts/wiki)
- [让你的 Mac 通知中心变得更实用：Today Scripts \- 少数派](https://sspai.com/post/40169)
- [用终端命令定制你的 OS X 通知中心：Today Scripts 体验详解 \- 少数派](https://sspai.com/post/27662)
- [Today Scripts：打造个性化 Yosemite 通知栏插件 \- Mac玩儿法](https://www.waerfa.com/today-scripts-for-yosemite-today-view)

## Battery status

```sh
full=$(pmset -g batt | { read; read n full; echo "$full"; })
batt=$(echo "$full" | awk '/(%);/{print $2}' | cut -d'%' -f1)
status=$(echo "$full" | cut -d';' -f2 | tr -d ' ')
time=$(echo "$full" | awk '/(%);/{print $4 " " $5}') #cut -d';' -f3 | sed 's/^ *//'
noc=$'\e[39m'


if   (($batt >= 66)); 
then battc=$'\e[32m';
elif (($batt >= 33)); 
then battc=$'\e[33m';
else battc=$'\e[31m';
fi;

if [ "$status" == "discharging" ]; then
    statc=$'\e[31m';
elif [ "$status" == "charging" ]; then
    statc=$'\e[32m';
elif [ "$status" == "charged" ]; then
    statc=$'\e[32m';
else
    statc=$'\e[33m';
fi

cyc_count=`ioreg -w0 -l | grep "Cycle Count" | awk 'BEGIN { FS = "=" } ; {print $8}' | awk 'BEGIN { FS = "}" } ; {print $1}'`

echo "$battc$batt%$noc"
echo "$statc$status$noc"
echo "$time" 
echo "$cyc_count cycles"
```

## IP address

```sh
echo -e "Local:    \c"
ipconfig getifaddr en0
echo -e "Gateway:  \c"
netstat -rn | grep default | grep en0 | awk '{print $2}'
echo -e "Public:   \c"
curl icanhazip.com
```

## Time zones

```sh
echo "Shanghai    `export TZ='Asia/Shanghai';date +'%H:%M';unset TZ`"
echo "Tokyo       `export TZ='Asia/Tokyo';date +'%H:%M';unset TZ`"
echo "Los Angeles `export TZ='America/Los_Angeles';date +'%H:%M';unset TZ`"
echo "Bonn        `export TZ='Europe/Berlin';date +'%H:%M';unset TZ`"
```
