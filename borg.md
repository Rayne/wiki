# Borg-Backup

## Create

```bash
export BORG_REPO="borg-reverse-tunnel:/var/backups/borg/example.borg"
export BORG_PASSPHRASE='example-123'
```

```bash
borg init -e repokey "$BORG_REPO"
```

```bash
borg create --stats --progress --compression zlib,6 "::{hostname}-{now}" "/root/docker.io/kanboard"
```

## Extract

```bash
borg extract --dry-run --list --strip-components 3 ::india.server.datenschuppen.de-2019-11-13T11:16:49 root/docker.io/kanboard
```

## Reverse Tunnel

```bash
ssh -R 10022:localhost:2222 remote
```
