---
weight: 400
title: "Vim"
---

References:

- [Editors (Vim) · the missing semester of your cs education](https://missing.csail.mit.edu/2020/editors/)
- `$ vimtutor`
- [Vim Tips Wiki | Fandom](https://vim.fandom.com/wiki/Vim_Tips_Wiki)

## General

General notes:

- `<C>`: `Ctrl` on Windows, `control` on Mac.
- `<Esc>`: `Esc` on Windows, `esc` on Mac.
    - Consider remapping `caps lock` to `esc`.
- If some command has a upper-case key, you should press at the same time `shift`.

`.vimrc` files from all three teachers:

- [dotfiles/.vimrc at master · JJGO/dotfiles](https://github.com/JJGO/dotfiles/blob/master/vim/.vimrc)
- [configs/init.vim at master · jonhoo/configs](https://github.com/jonhoo/configs/blob/master/editor/.config/nvim/init.vim)
- [dotfiles/vimrc at master · anishathalye/dotfiles](https://github.com/anishathalye/dotfiles/blob/master/vimrc)

```vim
" Save changes (write)
:w

" Close file (quit)
:q

" Close file without saving
:q!

" Help with some command
:help some command

" Enter normal mode
<Esc>
```

## Normal Mode

### Move Around

```vim
" One line up
k

" One line down
j

" One character left
h

" One character right
l
```

In-line:

```vim
" Next word's first letter (word)
w

" Next word's last letter (end)
e

" Previous word's first letter (back)
b

" Previous word's last letter
ge

" Beginning of the line
0

" First non-blank character of the line
^

" End of the line
$

" Jump between a pair of parentheses
%
```

Across lines:

```vim
" One screen up
<C>u

" One screen down
<C>d

" Beginning of the file
gg

" End of the file
G

" Last line on screen (low)
L

" Middle line on screen
M

" First line on screen (high)
H
```

### Search

In line:

```vim
" First instance of some character (example: first o)
fo

" Last instance of some character (example: first o)
Fo
```

In whole file:

```vim
" Search text
/text here

" Go to next match
n

" Go to previous match
N
```

### Edit

Basics:

```vim
" Delete the character under cursor
x

" Flip text case
~

" Repeat last change (after moving to another position)
.

" Undo
u

" Undo the whole line
U

" Redo
<C>r
```

Combined with content change:

```vim
" Replace the character under cursor with another character (example: o)
ro
```

Combined with movement:

```vim
" Delete (example: current word)
dw

" Delete the whole line
dd

" Delete & enter insert mode (example: from cursor until the end of the word) (change)
ce

" Delete the whole line & enter insert mode
cc
```

Combined with modifier:

```vim
" Delete (example: everything inside []) (inside)
di[

" Delete (example: everything inside [], including []) (around)
da[

" Delete & enter insert mode (example: everything inside "")
ci"

" Delete & enter insert mode (example: everything inside "", including "")
ca"
```

### Copy & Paste

```vim
" Copy (example: current word)
yw

" Copy the whole line
yy

" Copy (example: from cursor until the end of the word)
ye

" Paste, or put what's just deleted below the cursor
p
```

## Insert Mode

Enter insert mode:

```vim
" Directly (cursor stays at current position)
i

" Append (cursor goes one slot ahead)
a

" Open new line below cursor
o

" Open new line at cursor
O
```

## Visual Mode (Selection Mode)

Enter visual mode:

```vim
" Visual mode
v

" Visual line mode
V

" Visual block mode
<C>v
```

Copy & return to normal mode:
```vim
y
```

## Windows (Panels) & Tabs

Windows (panels):

```vim
" Open horizontal panel with the same file (split)
:sp

" Close current panel
:q

" Save all panels (write all)
:wa

" Close all panels (quit all)
:qa
```

Tabs:

```vim
" Open new tab
:tabnew
```
