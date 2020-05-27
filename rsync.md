# rsync

-   `-a` / `--archive` / `-rlptgoD`

-   `--bwlimit` limits the maximum transfer rate,
    e.g. `--bwlimit=5000` (5000 KB/s) and `--bwlimit=2.5m`

-   `-h` / `--human-readable`

-   `-i` / `--itemize-changes` outputs a change-summary for all updates

-   `-P` / `--partial --progress` keeps partially synchronized files
    and displays the transfer progress

-   `--stats` gives file transfer statistics,
    including the speed-up information and total size

-   `-z` compresses file data during the transfer

## Copy

```bash
rsync -azhP --stats --append-verify 2019-12-18\ Finroc+Eclipse-VM.7z neptun:
```

## Mirror

⚠️ **Caution**:
The following snippet _deletes data from the destination_ that is not available at the source.

```bash
rsync -azhP --stats --append-verify --delete hs:~/EXT/Backup/ ./Backup
```
