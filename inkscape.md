# Inkscape

Für SVG-Minimierung ist das Argument `--vacuum-defs` interessant.

## Export

### PNG

```bash
inkscape --export-area-page    --export-width=256 -z --file="$f" --export-png="${f:0:-4}".png
```

### PDF

```bash
inkscape --export-area-page    -z --file="$f" --export-pdf="${f:0:-4}".pdf
```

### LaTeX

```bash
inkscape --export-area-drawing -z --file="$f" --export-pdf="${f:0:-4}".pdf --export-latex
```
