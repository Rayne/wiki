# ffmpeg

## Einfache Konkatinierung

Siehe [Concatenate](https://trac.ffmpeg.org/wiki/Concatenate).

```bash
ffmpeg -f concat -safe 0 -i concat.txt  output.mp4
```

Benötigt `concat.txt`:

```
file 'A.webm'
file 'B.webm'
```

## Einfaches Skalierung

Mit Beibehaltung des Seitenverhältnisses:

```
ffmpeg -i input.jpg -vf scale=320:-1 output_320.png
```

## Rotation

```
ffmpeg -vfilters rotate=90 -i input.mp4 output.mp4
```

## GIF

Siehe [How do I convert a video to GIF using ffmpeg, with reasonable quality?](https://superuser.com/q/556029/99746).

```bash
ffmpeg -i "$INPUT" -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 "$INPUT.ffmpeg.gif"
ffmpeg -i "$INPUT" -vf "fps=10,scale=320:-1:flags=lanczos" -c:v pam -f image2pipe - | convert -delay 10 - -loop 0 -layers optimize "$INPUT.convert.gif"
```

## Meta-Daten

```bash
ffprobe -v quiet "$file" -print_format json -show_entries stream=index,codec_type:stream_tags=creation_time:format_tags=creation_time | grep creation_time
```

## Microsoft Powerpoint 2010

```bash
ffmpeg -i input.flv \
	-c:v wmv2 -q:v 4  \
	-c:a wmav2 -b:a 128k \
	output.wmv # avi
```

## Schnipsel

```bash
ffmpeg -i qualle.webm -ss AnfangInSekunden -t LängeInSekunden -c:v copy -c:a copy output.webm
```

**WEBM**

```bash
ffmpeg -i in.mp4 -b:v 2M -c:v libvpx -c:a libvorbis out.webm
```

**Bildschirm aufnehmen**

```bash
ffmpeg -f alsa -ac 2 -i pulse -f x11grab -r 25 -s 1280x720 -i :0.0 -c:v libx264 -pix_fmt yuv420p -preset ultrafast -crf 0 -threads 0 -acodec pcm_s16le -y out.mkv
```

**Skalierung + Wasserzeichen**

```bash
ffmpeg -i in.mp4 -c:v libvpx -b:v 3M -an -vf "movie=watermark.png [watermark]; [in]scale=-1:720[middle];[middle][watermark] overlay=main_w-overlay_w-10:main_h-overlay_h-10 [out]" ~/out.webm
```

**Schneiden ohne Re-Encoding**

```bash
ffmpeg -ss "$startSekunde" -i in.webm -t "$dauerSekunden" -c copy out.webm
```

**Zeitraffer**

```bash
ffmpeg -i in.mkv -r 30 -crf 30 -b:v 10M -filter:v "setpts=PTS/$speedupFactor" -an out.webm
```
