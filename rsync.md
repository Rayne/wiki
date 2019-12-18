# rsync

```
rsync -4 --partial --progress --append-verify 2019-12-18\ Finroc+Eclipse-VM.7z neptun:
```

-   One could also use `-P`, which is equivalent to `--partial --progress`

-   The maximum transfer rate can be limited with `--bwlimit`,
    e.g. `--bwlimit=5000` (5000 KB/s) and `--bwlimit=2.5m`
