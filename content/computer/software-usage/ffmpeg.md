---
weight: 400
title: "ffmpeg"
---

## Convert

### Video --> Audio

Credit: [How can I extract audio from video with ffmpeg? - Stack Overflow](https://stackoverflow.com/a/27413824)

```sh
ffmpeg -i input_video.mp4 -vn -acodec copy output_audio.m4a
```

Batch extract while preserving the file names: \([credit](https://stackoverflow.com/a/49092133)\)

```sh
for f in *.mp4; do ffmpeg -i "$f" -vn -acodec copy "${f%.mp4}".m4a; done
```

### Remove audio track from video \(aka mute\)

Credit: [How to remove an audio track from an mp4 video file? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/a/33864)

```sh
ffmpeg -i input_file.mp4 -vcodec copy -an output_file.mp4
```

### GIF --> video

Credit: [video - How to do I convert an animated gif to an mp4 or mv4 on the command line? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/a/294892) 

```sh
ffmpeg -i input_file.gif -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" output_file.mp4
```

Batch convert:

```sh
for f in *.gif; do ffmpeg -i "$f" -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" "${f%.gif}".mp4; done
```

### `.mov` --> `.mp4`

Credit: [converter - ffmpeg - Converting MOV files to MP4 - Stack Overflow](https://stackoverflow.com/a/12026739)

```sh
ffmpeg -i input.mov -q:v 0 output.mp4
```

### `.webm` --> `.mp4`

Credit: [webm to mp4 conversion using ffmpeg - Stack Overflow](https://stackoverflow.com/a/65996556)

```sh
ffmpeg -i vid.webm output.mp4
```

### `.m4a` --> `.mp3`

Credit: [audio - FFMPEG: Convert m4a to mp3 without significant loss - Super User](https://superuser.com/questions/704493/ffmpeg-convert-m4a-to-mp3-without-significant-loss)

```sh
ffmpeg -i input.m4a -c:v copy -c:a libmp3lame -q:a 4 output.mp3
```

### Video --> H.264 encoded \(iMovie compatible\)

Credit: [ffmpeg - Converted MP4 video file to H.264, but there is no sound - Super User](https://superuser.com/a/1325307)

```sh
ffmpeg -i input.mp4 -vcodec libx264 -acodec aac output.mp4
```

Batch convert:

```sh
for f in *.mp4; do ffmpeg -i "$f" -vcodec libx264 -acodec aac "${f%.mp4}"-encoded.mp4; done
```

## Compress video

Credit: [How can I reduce a video's size with ffmpeg? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/a/38380)

```sh
ffmpeg -i input.mp4 -vcodec libx264 -crf 24 output.mp4
```

Batch convert: 

```sh
for f in *.mp4; do ffmpeg -i "$f" -vcodec libx264 -crf 24 "${f%.mp4}"-compressed.mp4; done
```

## Merge Multiple Audio Files

Credit: [linux - Join many MP3, OGG, and FLAC files into one WAV or FLAC - Super User 
](https://superuser.com/a/584122)

The `-safe 0` is necessary because [ffmpeg will complain](https://stackoverflow.com/a/38999363).

```sh
# make a list of needed files
for f in ./*.flac; do echo "file '$f'" >> inputs.txt; done

# merge them
ffmpeg -f concat -safe 0 -i inputs.txt output.flac
```
