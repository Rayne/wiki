# convert

## Blur

```bash
convert -scale 320x -blur 0x8 "$in" "$out"
```

## Crop

```bash
convert "$f" -crop 0x0+1850-1243 +repage -resize 800x "${f:0:-4}".crop.png; done
```

Wenn man nur `320x240` angeben würde,
so würde das Bild in viele Einzelbilder zerlegt werden.

## Split

```bash
convert "$file" -rotate 90 -crop 2x1@  +repage "$file"
```
