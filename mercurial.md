# Mercurial / HG

## Commits

### Amend last commit

Analog zu `git commit --amend`:

```bash
hg commit --amend
```

### Undo last commit

Analog zu `git reset HEAD^:`

```bash
hg strip --keep --rev .
```

- [Quelle](https://stackoverflow.com/a/31277388)
- `--keep`: do not modify working directory during strip
- `--rev .` (the dot denotes the last commit. read sid0's answer regarding descendants)

## Configuration

### Encrypted Passwords

Instead of storing passwords in the `~/.hgrc` file, one can store account information in a keyring.
The following lines have to be added to the `~/.hgrc` configuration file to load the keyring extension.

```text
[extensions]
mercurial_keyring =
```

### Global `.hgignore`

Add to `~/.hgrc`:

```text
[ui]
ignore = ~/.hgignore
```
