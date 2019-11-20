# Shell

```
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

```
exec > >(tee -i log)
exec 2>&1
```

## Process Priorities

```
nice -n 19 ionice -c3 rm -rf /dir
```
