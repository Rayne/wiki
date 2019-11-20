# Docker

## IPs

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' kanboard_kanboard_1
```

The result can be used to directly communicate with the provided services,
e.g. with `wget IP`.

## Workdir Data

```bash
docker run -ti --rm --user 1002:1002 -v "$PWD:/data" php:7.4.0RC1-cli php /data/example.php
```
