---
weight: 400
title: "Sublime Text"
---

# Sublime Text

## Settings

<!-- <span class="gist__name">Preferences.sublime-settings<span class="gist__name--lang">json</span></span> -->

```json {hl_lines="16"}
{
    "added_words":
    [
        "wiki", // 拼写检查时忽略的词语
    ],
    "indent_guide_options":
    [
        "draw_active"
    ],
    "match_brackets": false,
    "match_brackets_braces": false,
    "match_brackets_content": false,
    "match_brackets_square": false,
    "mde.auto_fold_link.enabled": false,
    "open_files_in_new_window": false,
    "save_on_focus_lost": true, // 自动保存，很重要！
    "scroll_past_end": true,    // 打字机模式
    "shift_tab_unindent": true,
    "show_encoding": true,
    "show_full_path": true,
    "show_legacy_color_schemes": true,
    "show_line_endings": true,
    "show_navigation_bar": false,
    "spell_check": true,
    "tab_size": 4,
    "theme": "Default.sublime-theme",
    "translate_tabs_to_spaces": true,
    "tree_animation_enabled": false,
    "trim_trailing_white_space_on_save": "not_on_caret",
    "update_check": false,
    "word_wrap": true,
}
```

## Packages

[sublimetext - What is the most practical way to list all the installed packages in Sublime Text 3? - Stack Overflow](https://stackoverflow.com/a/30006324)

<!-- <span class="gist__name">Package Control.sublime-settings<span class="gist__name--lang">json</span></span> -->

```json
{
    "bootstrapped": true,
    "in_process_packages":
    [
    ],
    "installed_packages":
    [
        "A File Icon",
        "AutoDocstring",
        "BracketHighlighter",
        "Carbon",
        "ChineseLocalizations",
        "Codecs33",
        "Color Scheme - Legacy",
        "ColorHelper",
        "ConvertToUTF8",
        "CSS3",
        "Dracula Color Scheme",
        "Emmet",
        "FileSystem Autocompletion",
        "Fortran",
        "HTML-CSS-JS Prettify",
        "Indent XML",
        "INI",
        "LaTeXTools",
        "LockTab",
        "MarkdownEditing",
        "MarkdownPreview",
        "MarkdownTOC",
        "Outline",
        "Package Control",
        "Poppins - Color Scheme",
        "Pretty JSON",
        "Python Flake8 Lint",
        "R-Box",
        "rainbow_csv",
        "Sass",
        "SCSS",
        "SendCode",
        "Simple Print Function",
        "SublimeREPL",
        "SublimeTmpl",
        "Terminus",
        "TOML",
        "Typewriter",
        "VimL",
    ],
    "repositories":
    [
    ],
}
````


## Custom syntax

{{< gist
gist="f41e2945d5d7bb4245cd9cdad61d05f4"
file="GAUSS.sublime-syntax"
lang="yaml" >}}
