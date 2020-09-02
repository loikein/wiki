# tmux

References:

- [Command-line Environment · the missing semester of your cs education](https://missing.csail.mit.edu/2020/command-line/#terminal-multiplexers)
- [Home · tmux/tmux Wiki](https://github.com/tmux/tmux/wiki)
- [Tmux Cheat Sheet & Quick Reference](https://tmuxcheatsheet.com/)
- [tmux(1) - Linux manual page](https://man7.org/linux/man-pages/man1/tmux.1.html)
- [Tmux 使用教程 - 阮一峰的网络日志](https://www.ruanyifeng.com/blog/2019/10/tmux.html)

Note: consider changing the default key binding (`<C>a`) on local machine to work more smoothly on remote machines.

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

- Detach: `<C>b d`

## Window (Tab)

- Create new window: `<C>b c`
- Rename current window: `<C>b ,`
- Go to window by order: `<C>b 0`, `<C>b 1`, etc.
- Go to previous window: `<C>b p`
- Go to next window: `<C>b n`

## Panes

- Split current window into horizontal panes: `<C>b "`
- Split current window into vertical panes: `<C>b %`
- Move between panes: `<C>b direction-key`
- Zoom in & out to a pane: `<C>b z`
- Change pane size: `<C>b <C>direction-key`

## Configuration

### Scroll

Credit: [How do I scroll in tmux? - Super User](https://superuser.com/a/510310)

```vim
set -g mouse on
```
