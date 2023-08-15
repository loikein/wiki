---
weight: 400
title: "Blender"
---
[Blender 3.6 Reference Manual — Blender Manual](https://docs.blender.org/manual/en/3.6/index.html)

## Basic operations

### Mouse

macOS with trackpad:

- One finger click = {{< kbd `LMB` >}}
- Two finger drag = {{< kbd `MMB` >}}
- Two finger click = {{< kbd `RMB` >}}

{{< kbd `MMB` >}} operations: \(no need to use Emulate 3 Button Mouse\)

- Rotate: two finger drag
- Pan: {{< kbd `shift` >}} \+ two finger drag
- Zoom: {{< kbd `command` >}} \+ two finger drag

### Axes

- `X`: (+)Right (-)Left
- `Y`: (+)Back (-)Front
- `Z`: (+)Top (-)Bottom

### Views

Only add macOS shortcut when the key has a different name. Layout is US ANSI.

Turning on Emulate Numpad.

| Function | Windows | macOS |
|:---------|:--------|:------|
| View switcher | {{< kbd `~` >}} |  |
| View everything | {{< kbd `Home` >}} | {{< kbd `fn` `←` >}} |
| Front view | {{< kbd `1` >}} |    |
| Right view | {{< kbd `3` >}} |    |
| Top view | {{< kbd `7` >}} |    |
| Flip view along current axis | {{< kbd `9` >}} |    |
| Camera view | {{< kbd `0` >}} |    |
| Toggle local view | {{< kbd `/` >}} |    |
| Toggle Perspective/Orthographic | {{< kbd `5` >}} |    |

<!-- `If you reset your camera rotation ( alt-r ) `??? -->

### Selection

| Function | Windows | macOS |
|:---------|:--------|:------|
| Change selection | {{< kbd `W` >}} |    |
| Move | {{< kbd `G` >}} |    |
| Scale | {{< kbd `S` >}} |    |
| Rotate | {{< kbd `R` >}} |    |
| Delete | {{< kbd `X` >}} |    |
| Loop select | {{< kbd `Alt` `LMB` >}} | {{< kbd `option` `LMB` >}} |
| Selected items to collection | {{< kbd `M` >}} |    |


### Item operation \(Object Mode\)

| Function | Windows | macOS |
|:---------|:--------|:------|
| Add item | {{< kbd `Shift` `A` >}} |    |
| Show operator panel | {{< kbd `F9` >}} |    |
| Hide item | {{< kbd `H` >}} |    |


### Item operation \(Edit Mode\)

| Function | Windows | macOS |
|:---------|:--------|:------|
| Unhide all items | {{< kbd `Alt` `H` >}} | {{< kbd `option` `H` >}} |
| Loop cut | {{< kbd `Ctrl` `R` >}} | {{< kbd `command` `R` >}} |
| Edge crease | {{< kbd `Shift` `E` >}} |    |
| Insert face | {{< kbd `I` >}} |    |

### Modes

| Function | Windows | macOS |
|:---------|:--------|:------|
| Go back to previous mode | {{< kbd `Tab` >}} |    |
| Center to 3D Cursor | {{< kbd `Shift` `C` >}} |    |


## Camera

When adjusting camera, use {{< kbd `N` >}} Menu ▸ View ▸ Lock Camera to View


## Modifiers

- Permanently fix a modifier by Apply.
- Bevel: Remember to \(in Object Mode ▸ {{< kbd `Ctrl` `A` >}}\) apply scale
- Mirror: Remember to \(in Object Mode ▸ {{< kbd `RMB` >}}\) set origin \(to 3D Cursor, for example\)
- Subdivision Surface: Make object look smoother
- Solidify: Give thickness to face \(face → object\)


## HDRI

- [HDRIs • Poly Haven](https://polyhaven.com/hdris)


## Tutorials

- [x] [【Blender】初心者向け！Blender超入門講座　～簡単なセルルックのうさぎのキャラクターを作ろう！～ - YouTube](https://www.youtube-nocookie.com/embed/OoM0ikOi1v4?cc_load_policy=1&hl=en)
    + Notes: Preferences, basic operations, modifiers \(Mirror, Subdivision Surface\), [proportional editing](https://docs.blender.org/manual/en/3.6/editors/3dview/controls/proportional_editing.html), material \(node mode\)
- [x] [【初心者向け】世界一やさしいBlender入門！使い方＆導入〜画像作成までを徹底解説【3.3対応】 - YouTube](https://www.youtube-nocookie.com/embed/S6aAvxUx2ko?cc_load_policy=1&hl=en)
    + Notes: Slightly harder boxes stacking; basic lighting \& camera
- [x] [【blender】おたまを超簡単モデリング！ - YouTube](https://www.youtube-nocookie.com/embed/nnc80zpAOD0)
    + Notes: Solidify; HDRI environment background in render \(file used in video: 2K version of [Venetian Crossroads HDRI](https://polyhaven.com/a/venetian_crossroads)\)
    + This video goes really fast and I had to pause very often to follow.

<!-- 
- [ ] [If I Started Blender In 2023, I'd Do This - YouTube](https://www.youtube-nocookie.com/embed/1WOVNkJQEAQ?cc_load_policy=1&hl=en)
- [ ] [I animated this in 18 days... in Blender - YouTube](https://www.youtube-nocookie.com/embed/tCTkkHGRpNk?cc_load_policy=1&hl=en)
- [ ] Introduction to Blender 3.0: Learn Organic and Architectural Modeling, Lighting, Materials, Painting, Rendering, and Compositing with Blender \([companion files](https://github.com/Apress/Introduction-to-Blender-3.0)\)
- [ ] [Immersive Math](https://immersivemath.com/ila/)
 -->
