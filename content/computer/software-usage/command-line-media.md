# Media Related Shell Commands

## dwebp

Online manual: [dwebp(1) — Arch manual pages](https://man.archlinux.org/man/dwebp.1.en)

Credit: [How to Convert WebP to PNG in Linux](https://winaero.com/convert-webp-png-linux/)

```bash
$ dwebp pic.webp -o pic.png
```

## convert (imagemagick)

Online manual: [convert(1) - Linux man page](https://linux.die.net/man/1/convert)

### Convert SVG

Original size: ([credit](https://stackoverflow.com/a/18579465))

```bash
$ convert -background none pic.svg pic.png
```

Given PPI: ([credit](https://stackoverflow.com/a/57512918))

Reference: [ImageMagick - Command-line Options #density](https://imagemagick.org/script/command-line-options.php#density)

```bash
$ convert -density 300 pic.svg pic.png
```

### Trim transparent part of png

Credit: [ubuntu - how to cut transparent part from photo with command or shell script - Stack Overflow](https://stackoverflow.com/a/52829809)

Need to read:

- [Rule of thumb: When to use +repage? - ImageMagick](https://legacy.imagemagick.org/discourse-server/viewtopic.php?t=35826)
- [Cutting and Bordering -- IM v6 Examples](https://legacy.imagemagick.org/Usage/crop/)
- [Basic Usage -- IM v6 Examples](https://legacy.imagemagick.org/Usage/basics/)


```bash
$ convert -fuzz 25% -trim +repage pic.png pic-trim.png
```

Batch trim:

```bash
$ for f in *.png;  do convert -fuzz 25% -trim +repage "$f" "${f%.png}-trim".png; done
```
