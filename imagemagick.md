# ImageMagick

## Export ICO

```
convert "$file" -define icon:auto-resize=256,128,64,48,32,16 "$file.ico"
```

## Export JPEG

```bash
convert "$file" -resize "${size}x${size}>" -quality "$quality" -sampling-factor 4:2:0 "${file:0:-4}.out.jpg"
```

## Remove Background from Scans

```bash
convert "$file" -fuzz 25% -fill white -opaque \#f6fbff "${file:0:-4}.out.png"
```

## Split landscape image

```bash
convert "$file" -rotate 90 -crop 2x1@  +repage "$file"
```
