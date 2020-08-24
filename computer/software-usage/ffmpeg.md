# ffmpeg

## Extract audio from video

Credit: [How can I extract audio from video with ffmpeg? - Stack Overflow](https://stackoverflow.com/a/27413824)

```bash
$ ffmpeg -i "input-video.mp4" -vn -acodec copy output-audio.m4a
```

Batch extract while preserving the file names: \([credit](https://stackoverflow.com/a/49092133)\)

```bash
$ for f in *.mp4;  do ffmpeg -i "$f" -vn -acodec copy "${f%.mp4}".m4a;  done
```
