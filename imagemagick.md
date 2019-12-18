# ImageMagick

## Export JPEG

```bash
convert "$file" -resize "${size}x${size}>" -quality "$quality" -sampling-factor 4:2:0 "${file:0:-4}.out.jpg"
```

## Remove Background from Scans

```bash
convert "$file" -fuzz 25% -fill white -opaque \#f6fbff "${file:0:-4}.out.png"
```
