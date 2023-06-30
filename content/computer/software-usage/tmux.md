---
weight: 400
title: "tmux"
---

References:

- [Command-line Environment · the missing semester of your cs education](https://missing.csail.mit.edu/2020/command-line/#terminal-multiplexers)
- [Home · tmux/tmux Wiki](https://github.com/tmux/tmux/wiki)
- [Tmux Cheat Sheet & Quick Reference](https://tmuxcheatsheet.com/)
- [tmux(1) - Linux manual page](https://man7.org/linux/man-pages/man1/tmux.1.html)
- [Tmux 使用教程 - 阮一峰的网络日志](https://www.ruanyifeng.com/blog/2019/10/tmux.html)
- [The best and greatest tmux.conf ever](https://gist.github.com/spicycode/1229612)

## Session

In shell:

```sh
# New session (s for session)
$ tmux new -s my-session

# Re-attach to existing session (t for target)
$ tmux attach -t my-session
$ tmux a -t my-session

# Stop a session
$ tmux kill-session -t my-session

# List all Tmux sessions
$ tmux ls
```

In Tmux sessions:

- Detach current session: `<C>b d`
- Rename current session: `<C>b $`

## Window (Tab)

- Create new window: `<C>b c`
- Close current window: `<C>b &`
- Rename current window: `<C>b ,`
- Go to window by order: `<C>b 0`, `<C>b 1`, etc.
- Go to previous window: `<C>b p`
- Go to next window: `<C>b n`

## Panes

- Split current window into horizontal panes \(`=`\): `<C>b "`
- Split current window into vertical panes \(`||`\): `<C>b %`
- Close current pane: `<C>b x`
- Move between panes: `<C>b direction-key`
- Zoom in & out to a pane: `<C>b z`
- Change pane size: `<C>b <C>direction-key`

<!-- - Rename current pane: `$ printf '\033]2;%s\033\\' 'title'` -->

## Configuration

### Change Prefix Key

In `.tmux.conf`:

```text
# Remap prefix from 'C-b' to 'C-a'
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix
```

### Change Shortcut Key

For example, in `.tmux.conf`:

```text
# Split panes using | and -
bind | split-window -h
bind - split-window -v
unbind '"'
unbind %
```

### 256 Colour

Set alias \(in `.zshrc`\): \([credit](https://unix.stackexchange.com/a/355391)\)

```bash
alias tmux='tmux -2'
```

In `.tmux.conf`:

```text
set -g default-terminal "screen-256color"
```

### Scroll & Click to Switch Panes

Credit: [How do I scroll in tmux? - Super User](https://superuser.com/a/510310)

```text
set -g mouse on
```

### Automatically Rename Window

In `.tmux.conf`: \([credit](https://stackoverflow.com/a/45010147)\)

```text
# Automatically rename status
set-option -g status-interval 5
set-option -g automatic-rename on
set-option -g automatic-rename-format '#{b:pane_current_path}'
```
