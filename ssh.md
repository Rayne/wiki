# SSH

## Port-Forwarding

```bash
ssh -L 3306:localhost:3306 ds3
```

## SOCKS-Proxy

```bash
ssh -D 8080 ds3
```

## Reverse-Proxy

1.	Specify a reverse proxy at port 43022
	that is tunneling to port 22 of the client.

	```bash
	ssh -R 43022:localhost:22 india
	```

2.	Connect to the reverse proxy to gain local access.
	This step has to be executed on the remote system.

	```bash
	ssh localhost -p 43022
	```
