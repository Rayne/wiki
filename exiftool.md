# exiftool

```bash
time="2014:01:31 11:47:31"
exiftool -m -XMPToolkit= -alldates="$time" -DateTimeDigitized="$time" -ModifyDate= file.jpg
```

## Set Creation Time with _Ymd His_ Format

```bash
exiftool -DateTimeOriginal="2024:04:27 20:00:00"
```

## Rename images with meta-data

The following snippet is directly based on the manual.

```bash
exiftool '-FileName<DateTimeCreated' -d '%Y-%m-%d %H-%M-%S%%-c.%%e' "$file"
exiftool '-FileName<CreateDate'      -d '%Y-%m-%d %H-%M-%S%%-c.%%e' "$file"
```

When a camera was configured with a wrong date, we need to modify the timestamp first.
It would be also a good idea to update the timestamp, but the following snippet does not modify it.

```bash
date="$(exiftool -tab -dateFormat '%Y-%m-%d %H:%M:%S' -Exif:CreateDate "$file" | cut -f 2)"

# With time zone offset of 1 hour and 18 minutes:
date="$(date -d "$date +0118" '+%Y-%m-%d %H-%M-%S')"

destination="$date $file"

if [[ -f "$destination" ]]; then
    echo "File exists already: $destination"
    exit 2
fi

mv "$file" "$date $file"
```
