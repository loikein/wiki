---
weight: 400
title: "Sublime Text 3 & 4"
---

## Settings

<!-- <span class="gist__name">Preferences.sublime-settings<span class="gist__name--lang">json</span></span> -->

```json
{
    "added_words":
    [
        "wikipedia",                        // 拼写检查时检查的词语
    ],

    "atomic_save": true,
    "auto_complete_size_limit": 1000,
    "auto_complete_commit_on_tab": true,
    "color_scheme": "Packages/User/Poppins.tmTheme",
    "draw_white_space": "all",
    "enable_tab_scrolling": false,          // 显示所有标签页
    "ensure_newline_at_eof_on_save": true,  // 在文档末尾添加回车
    "font_face": "Menlo",
    "font_size": 15,
    "git_diff_target": "head",
    "hide_tab_scrolling_buttons": true,
    "hide_new_tab_button": true,
    "ignored_words":
    [
        "nonlinear",                        // 拼写检查时忽略的词语
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
    "save_on_focus_lost": true,             // 自动保存
    "scroll_past_end": true,                // 类似打字机模式
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
    "highlight_modified_tabs": true,
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

### HTML-CSS-JS Prettify

User setting:

```json
{
    "all": {
        "preserve_newlines": false,
    },
    "css": {
        "indent_size": 2,
    }
}
```


## Custom syntax highlighting

> In Sublime Text 4, if you have more than one custom syntaxes, they will show up as a single `User` syntax group in the syntax selector.
{.book-hint .info}

### GAUSS

Written by myself when dealing with the [BLP-1999](https://github.com/loikein/BLP-1999-archive) files. Marginally better than nothing.

`GAUSS.sublime-syntax`:

```yaml
%YAML 1.2
---
# See http://www.sublimetext.com/docs/3/syntax.html
file_extensions:
  - gss, prg, arc
scope: source.GAUSS
contexts:
  main:
    # Strings begin and end with quotes, and use backslashes as an escape
    # character
    - match: '"'
      scope: punctuation.definition.string.begin.GAUSS
      push: double_quoted_string

    # Comments begin with a '/*' and finish at the end of the line
    - match: '\/\*'
      scope: punctuation.definition.comment.GAUSS
      push: line_comment

    # Comments begin with a '@' and finish at the end of the line
    - match: '@.*@'
      scope: punctuation.definition.comment.GAUSS
      push: line_comment

    # Block comments begin with a '@'
    - match: '@.*\n'
      scope: punctuation.definition.comment.begin.GAUSS
      push: begin_block_comment

    # # Block comments end with a '@'
    # - match: '^@$'
    #   scope: punctuation.definition.comment.end.GAUSS
    #   push: end_block_comment


    # Keywords are if, else for and while.
    # Note that blackslashes don't need to be escaped within single quoted
    # strings in YAML. When using single quoted strings, only single quotes
    # need to be escaped: this is done by using two single quotes next to each
    # other.
    - match: '\b(if|if not|else|elseif|for|while|do until|endif|endo|proc|retp|endp)\b'
      scope: keyword.control.GAUSS

    # Numbers
    - match: '\b(-)?[0-9.]+\b'
      scope: constant.numeric.GAUSS

    # Brackets
    - match: \(
      push: brackets
    - match: \)
      scope: invalid.illegal.stray-bracket-end

  double_quoted_string:
    - meta_scope: string.quoted.double.GAUSS
    - match: '\\.'
      scope: constant.character.escape.GAUSS
    - match: '"'
      scope: punctuation.definition.string.end.GAUSS
      pop: true

  line_comment:
    - meta_scope: comment.line.GAUSS
    - match: $
      pop: true

  begin_block_comment:
    - meta_scope: comment.begin.GAUSS
    - match: $
      pop: true

  # end_block_comment:
  #   - meta_scope: comment.end.GAUSS
  #   - match: $
  #     pop: true

  brackets:
    - match: \)
      pop: true
    - include: main
```

### Hugo

Refs:

- [Go HTML template syntax highlighting for Sublime Text](https://gist.github.com/jozsefsallai/5b09fb0099158344512aaec8121220a1)
- [DisposaBoy/GoSublime: A Golang plugin collection for SublimeText 3, providing code completion and other IDE-like features.](https://github.com/DisposaBoy/GoSublime)

{{< gist
gist="5b09fb0099158344512aaec8121220a1"
file="GoHTML.sublime-syntax"
lang="yaml" >}}

{{< gist
gist="5b09fb0099158344512aaec8121220a1"
file="GoTemplate.sublime-syntax"
lang="yaml" >}}
