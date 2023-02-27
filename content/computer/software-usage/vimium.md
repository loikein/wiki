# Vimium

Reference: [philc/vimium: The hacker's browser.](https://github.com/philc/vimium)

First of all:

```text
?       show the help dialog for a list of all available keys
```

## Inside Current Tab

```text
h       scroll left
j       scroll down
k       scroll up
l       scroll right
gg      scroll to top of the page
G       scroll to bottom of the page
d       scroll down half a page
u       scroll up half a page

r       reload
gs      view source
i       enter insert mode -- all commands will be ignored until you hit Esc to exit

H       go back in history
L       go forward in history

yt      duplicate current tab

x       close current tab
X       restore closed tab (i.e. unwind the 'x' command)
```

### Search

```text
/       enter find mode
          -- type your search query and hit enter to search, or Esc to cancel
n       cycle forward to the next find match
N       cycle backward to the previous find match
```

## Going to New Tab

```text
f       open a link in the current tab
F       open a link in a new tab

o       Open URL, bookmark, or history entry
O       Open URL, bookmark, history entry in a new tab
b       Open bookmark
B       Open bookmark in a new tab

t       create tab
T       search through your open tabs
```

## Among Tabs

```text
J       go one tab left
K       go one tab right

^       visit the previously-visited tab
```
