# GIT

```bash
git config user.name John\ Doe
git config user.email "$USER@$HOSTNAME"
```

**Miscellaneous**

```bash
git config core.compression 0
git config pack.window 0
```

## .gitattributes

```
*.jpg binary -delta
*.jpeg binary -delta
```

## Custom Date

```bash
date="$(date -d "2019-06-20 19:12:36")"
export GIT_COMMITTER_DATE="$date"
export GIT_AUTHOR_DATE="$date"
```

## Pulled from Wrong Repository

```
git tag -l | xargs git tag -d # Delete all tags
git fetch --tags
git gc
git fsck
```
