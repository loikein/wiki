---
weight: 400
title: "Matrix/Element"
description: "Best dotfile manager ever."
---

# Matrix / Element

## Element

`/help`:

### 消息

```
/spoiler    <message>   Sends the given message as a spoiler
/shrug      <message>   Prepends ¯\_(ツ)_/¯ to a plain-text message
/tableflip  <message>   Prepends (╯°□°）╯︵ ┻━┻ to a plain-text message
/unflip     <message>   Prepends ┬──┬ ノ( ゜-゜ノ) to a plain-text message
/lenny      <message>   Prepends ( ͡° ͜ʖ ͡°) to a plain-text message
/plain      <message>   Sends a message as plain text, without interpreting it as markdown
/html       <message>   Sends a message as html, without interpreting it as markdown
/rainbow    <message>   Sends the given message coloured as a rainbow
/rainbowme  <message>   Sends the given emote coloured as a rainbow
/me         <message>   Displays action
```

### 动作

```
/nick       <display_name>          Changes your display nickname
/myroomnick <display_name>          Changes your display nickname in the current room only
/roomavatar [<mxc_url>]             Changes the avatar of the current room
/myroomavatar   [<mxc_url>]         Changes your avatar in this current room only
/myavatar   [<mxc_url>]             Changes your avatar in all rooms
/invite     <user-id> [<reason>]    Invites user with given id to current room
/join       <room-address>          Joins room with given address
/part       [<room-address>]        Leave room
/ignore     <user-id>               Ignores a user, hiding their messages from you
/unignore   <user-id>               Stops ignoring a user, showing their messages going forward
/query      <user-id>               Opens chat with the given user
/msg        <user-id> [<message>]   Sends a message to the given user
```

### 管理员

```
/upgraderoom    <new_version>       Upgrades a room to a new version
/topic          [<topic>]           Gets or sets the room topic
/roomname       <name>              Sets the room name
/remove         <user-id> [reason]  Removes user with given id from this room
/ban            <user-id> [reason]  Bans user with given id
/unban          <user-id>           Unbans user with given ID
/addwidget      <url | embed code | Jitsi url>  Adds a custom widget by URL to the room
```

### 高级

```
/devtools       Opens the Developer Tools dialog
/verify         <user-id> <device-id> <device-signing-key>  Verifies a user, session, and pubkey tuple
/discardsession Forces the current outbound group session in an encrypted room to be discarded
/help           Displays list of commands with usages and descriptions
/whois          <user-id>       Displays information about a user
/rageshake      <description>   Send a bug report with logs
```

### 效果

```
/confetti       <message>   Sends the given message with confetti
/fireworks      <message>   Sends the given message with fireworks
/rainfall       <message>   Sends the given message with rainfall
/snowfall       <message>   Sends the given message with snowfall
/spaceinvaders  <message>   Sends the given message with a space themed effect
/hearts         <message>   Sends the given message with hearts
```

### 其他

```
/holdcall       Places the call in the current room on hold
/unholdcall     Takes the call in the current room off hold
/converttodm    Converts the room to a DM
/converttoroom  Converts the DM to a room
```
