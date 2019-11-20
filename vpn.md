# VPN

## OpenConnect

```bash
openconnect -u meckel@rhrk.uni-kl.de --authgroup Split_Tunnel vpn.uni-kl.de
```

Notwendige Angaben können auch interaktiv gesetzt werden:

```bash
openconnect vpn.uni-kl.de
```

```
POST https://vpn.uni-kl.de/
Verbunden mit [2001:638:208:fd40::6]:443
SSL-Verhandlung mit vpn.uni-kl.de
Verbunden mit HTTPS auf vpn.uni-kl.de
XML POST aktiviert
Please enter your username and password.
GROUP: [Full_Tunnel|Full_Tunnel_Local_LAN_Access|Split_Tunnel]:Split_Tunnel
POST https://vpn.uni-kl.de/
XML POST aktiviert
Please enter your username and password.
Username:meckel@rhrk.uni-kl.de
Password:
POST https://vpn.uni-kl.de/
CONNECT-Antwort erhalten: HTTP/1.1 200 OK
CSTP verbunden. DPD 30, Keepalive 20
Als 131.246.80.71 + 2001:638:208:fd4e::1082/64 verbunden, SSL wird verwendet
DTLS-Handshake schlug fehl: Error in the push function.
(Verhindert eine Firewall das Senden von UDP-Paketen?)
```
