# espanso

Reference: [Documentation - espanso - Cross-platform Text Expander written in Rust](https://espanso.org/docs/)

## Basics

User profile path: `~/Library/Preferences/espanso/`  
Config file: `~/Library/Preferences/espanso/default.yml`

To find out about this:

```bash
$ espanso path
```

## Options

### `word:true`

The difference introduced when using `word: true` option is that you will need to type an extra space before expanding. For example, if you write this:

```yaml
# in default.yml

matches:
  - trigger: ":email"
    word: true
    replace: "example@example.com"
```

then you will result in `example@example.com␣` ending with a space, which may not be recognised as a valid email address on some websites. Therefore, you may want to not to use the option.

## Match Examples

### Reading Notes

```yaml
  - trigger: ":book"
    word: true
    replace: |
      ## Reading note
      
      - Time: {{mydate}}
      - Author:
      - Title:
      - Page:
      - Notes:
    vars:
      - name: mydate
        type: date
        params:
          format: "%Y%m%d%H%M"
```

### Breadcrumb Trail

Credit: [Fun with espanso - Share & showcase - Obsidian Forum](https://forum.obsidian.md/t/fun-with-espanso/2317)

```yaml
  - trigger: ":bc"
    word: true
    replace: {{output}}
    vars:
      - name: output
        type: shell
        params:
          cmd: "echo `date -v -1d \"+[[%Y-%m-%d|<< Yesterday]]\"`' | '`date -v +1d \"+[[%Y-%m-%d|Tommorrow >>]]\"`"
```
