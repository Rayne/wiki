# Mercurial / HG

## Amend last commit

Analog zu `git commit --amend`:

```
hg commit --amend
```

## Undo last commit

Analog zu `git reset HEAD^:`

```
hg strip --keep --rev .
```

- [Quelle](https://stackoverflow.com/a/31277388)
- `--keep`: do not modify working directory during strip
- `--rev .` (the dot denotes the last commit. read sid0's answer regarding descendants)

## Global `.hgignore`

Add to `~/.hgrc`:

```
[ui]
ignore = ~/.hgignore
```
