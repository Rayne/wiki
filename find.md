# Find

## Find files by date

```bash
find -newermt $(date +%Y-%m-%d -d '1 day ago') -type f -print
```

See [Stackoverflow](https://stackoverflow.com/a/18705427).
