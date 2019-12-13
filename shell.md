# Shell

```bash
set -eux
shopt -s nullglob
```

## Parallelization

```bash
apt install parallel
```

```bash
find -iname '*png' -print0 | parallel -0 -j 8 optipng {}
```

## Log Input and Output

```bash
exec > >(tee -i log)
exec 2>&1
```

## Process Priorities

```bash
nice -n 19 ionice -c3 rm -rf /dir
```
