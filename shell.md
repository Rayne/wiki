# Shell

```bash
set -eux
shopt -s nullglob
```

## Documentation

- [BASH Frequently Asked Questions](http://mywiki.wooledge.org/BashFAQ)
- [Bash Hackers Wiki](https://wiki.bash-hackers.org)

## Articles

- [Introduction to Flock](https://linuxaria.com/howto/linux-shell-introduction-to-flock)

## Snippets

### Parallelization

```bash
apt install parallel
```

```bash
find -iname '*png' -print0 | parallel -0 -j 8 optipng {}
```

### Log Input and Output

```bash
exec > >(tee -i log)
exec 2>&1
```

### Process Priorities

```bash
nice -n 19 ionice -c3 rm -rf /dir
```

### Timestamps

```bash
date '+%Y-%m-%d'
date '+%Y-%m-%d %H:%M:%S'
date '+%Y-%m-%d_%H-%M-%S'
```
