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

## Convert video to H.264 encoded \(iMovie compatible\)

Credit: [ffmpeg - Converted MP4 video file to H.264, but there is no sound - Super User](https://superuser.com/a/1325307)

```bash
$ ffmpeg -i input.mp4 -vcodec libx264 -acodec aac output.mp4
```

Batch convert:

```bash
$ for f in *.mp4;  do ffmpeg -i "$f" -vcodec libx264 -acodec aac "${f%.mp4}"-encoded.mp4;  done
```

## Merge Multiple Audio Files

Credit: [linux - Join many MP3, OGG, and FLAC files into one WAV or FLAC - Super User 
](https://superuser.com/a/584122)

The `-safe 0` is necessary because [ffmpeg will complain](https://stackoverflow.com/a/38999363).

```bash
# make a list of needed files
$ for f in ./*.flac; do echo "file '$f'" >> inputs.txt; done

# merge them
$ ffmpeg -f concat -safe 0 -i inputs.txt output.flac
```
