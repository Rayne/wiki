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
borg create --stats --progress --compression zlib,9 --list --filter=AME "::{hostname}-{now}" "/root/docker.io/kanboard"
```

## Extract

```bash
borg extract --dry-run --list --strip-components 3 ::india.server.datenschuppen.de-2019-11-13T11:16:49 root/docker.io/kanboard
```

## Reverse Tunnel

```bash
ssh -R 10022:localhost:2222 remote
```

## Mount

```
borg mount REPOSITORY_OR_ARCHIVE MOUNTPOINT
borg umount MOUNTPOINT
```

## Bandwidth

### Upload

```
--remote-ratelimit
```

### Download

>	There is no built-in way to limit download (i.e. borg extract) bandwidth, but limiting download bandwidth can be accomplished with pipeviewer:
>
>	Create a wrapper script: /usr/local/bin/pv-wrapper
>
>	```
>	#!/bin/sh
>	# -q, --quiet              do not output any transfer information at all
>	# -L, --rate-limit RATE    limit transfer to RATE bytes per second
>	RATE=307200
>	pv -q -L $RATE  | "$@"
>	```
>
>	Add BORG_RSH environment variable to use pipeviewer wrapper script with ssh.
>
>	export BORG_RSH='/usr/local/bin/pv-wrapper ssh'
>
>	Now Borg will be bandwidth limited. Nice thing about pv is that you can change rate-limit on the fly:
>
>	pv -R $(pidof pv) -L 102400
>
>	-- https://borgbackup.readthedocs.io/en/stable/faq.html
