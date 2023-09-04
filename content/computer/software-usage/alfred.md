---
weight: 400
title: "Alfred"
---

## Run Script in Terminal

### iTerm

Credit: [custom-alfred-iterm-scripts/custom_iterm_script.applescript](https://github.com/vitorgalvao/custom-alfred-iterm-scripts/blob/master/custom_iterm_script.applescript)

```AppleScript
-- For the latest version:
-- https://github.com/vitorgalvao/custom-alfred-iterm-scripts

-- Set this property to true to always open in a new window
property open_in_new_window : false

-- Handlers
on new_window()
    tell application "iTerm" to create window with default profile
end new_window

on new_tab()
    tell application "iTerm" to tell the first window to create tab with default profile
end new_tab

on call_forward()
    tell application "iTerm" to activate
end call_forward

on is_running()
    application "iTerm" is running
end is_running

on has_windows()
    if not is_running() then return false
    if windows of application "iTerm" is {} then return false
    true
end has_windows

on send_text(custom_text)
    tell application "iTerm" to tell the first window to tell current session to write text custom_text
end send_text

-- Main
on alfred_script(query)
    if has_windows() then
        if open_in_new_window then
            new_window()
        else
            new_tab()
        end if
    else
        -- If iTerm is not running and we tell it to create a new window, we get two
        -- One from opening the application, and the other from the command
        if is_running() then
            new_window()
        else
            call_forward()
        end if
    end if

    -- Make sure a window exists before we continue, or the write may fail
    repeat until has_windows()
        delay 0.01
    end repeat

    send_text(query)
    call_forward()
end alfred_script
```

### alacritty

Only with workflow: [Running commands from Alfred · Issue #2638 · alacritty/alacritty](https://github.com/alacritty/alacritty/issues/2638#issuecomment-677601694)

## Custom Search

A curated list: [🎩 Alfred Custom Web Searches](https://alfred.pory.app/)

### explainshell

Does the same thing as [svsool/alfred-explainshell: Explain Shell workflow for Alfred](https://github.com/svsool/alfred-explainshell). \([credit](https://www.alfredforum.com/topic/3070-manpages-using-explainshellcom/?do=findComment&comment=21096)\)

```text
URL:             http://explainshell.com/explain?cmd={query}
Encode space as: +
Keyword:         es
```

### hndex

Full-text search engine for Hacker News.

```text
URL:             https://hndex.org/?q={query}
Encode space as: +
Keyword:         hn
```

### Linguee

Set the keyword the same as dictionary's shortcut to remind yourself there's that.

```text
URL:             https://www.linguee.com/english-chinese/search?source=auto&query={query}
Encode space as: +
Keyword:         d
```

### Reverso Context

```text
URL:             https://context.reverso.net/translation/english-chinese/{query}
Encode space as: +
Keyword:         d
```

### Google Translation

```text
URL:             https://translate.google.com/?sl=auto&tl=zh-CN&text={query}&op=translate
Encode space as: %20
Keyword:         tran
```

### DeepL Translation

```text
URL:             https://www.deepl.com/translator#de/zh/{query}
Encode space as: 
Keyword:         tran
```

## Useful Workflows

Workflow function requires a paid license. All tested with Alfred 4.1 on macOS 10.15.

### Bluetooth Controller

Repository: [vegardinho/alfred_bluetooth_controller: Alfred workflow for managing bluetooth settings and -connections](https://github.com/vegardinho/alfred_bluetooth_controller)

### Encode / Decode

Repository: [willfarrell/alfred-encode-decode-workflow: Encoding and decoding a sting into multiple variations.](https://github.com/willfarrell/alfred-encode-decode-workflow)

### Firefox Assistant

Repository: [deanishe/alfred-firefox: Search and control Firefox from Alfred](https://github.com/deanishe/alfred-firefox)  
Firefox add-on: [Alfred Integration](https://addons.mozilla.org/en-US/firefox/addon/alfred-launcher-integration/)

### Fn

Repository: [loikein/fn-alfred-workflow: An Alfred workflow to toggle MacBook Touch Bar status.](https://github.com/loikein/fn-alfred-workflow/tree/main)

I wrote this one under some peculiar situation where I had to switch back and forth.

However, you would probably be better-off by settling on one status \(recommendation: app with short controls\), and then configure applications where fn key row is always shown by going to System Preferences ▸ Keyboard ▸ Keyboard Shortcuts ▸ Function Keys.

### GitHub Repos

Repository: [edgarjs/alfred-github-repos: Alfred workflow to easily open Github repositories](https://github.com/edgarjs/alfred-github-repos)  
Packal: [Github Repos \| Packal](https://www.packal.org/workflow/github-repos-0)


### HTML link to RTF link

Not on GitHub yet.

Code:

```sh
query=$1

echo "$1" | textutil -stdin -format html -convert rtf -stdout | tee >(pbcopy -pboard general -Prefer public.rtf)
```

I wrote this with code from [Creating Rich Links in Keyboard Maestro | ThoughtAsylum](https://www.thoughtasylum.com/2022/02/26/creating-rich-links-in-keyboard-maestro/), and adjusted with [this answer](https://apple.stackexchange.com/a/444986) for Apple Notes.app custom RTF formatting.

### OmniFocus

Discussion thread & download link: [Adding tasks from Alfred 3? - OmniFocus - The Omni Group Forums](https://discourse.omnigroup.com/t/adding-tasks-from-alfred-3/35232/22)

My customisation:

```text
Placeholder Subtext: Flag! @Context ::Project (#Start #Due) $Duration //Note
```

### Search Notes

Repository: [sballin/alfred-search-notes-app: Use Alfred to quickly open notes in iCloud/Apple Notes.](https://github.com/sballin/alfred-search-notes-app)
