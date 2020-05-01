# VirtualBox

```bash
vboxmanage list vms
vboxmanage list hdds
vboxmanage showvminfo Finroc
```

## Guest Driver

```bash
apt install virtualbox-guest-x11-hwe
```

Die Installation ist auch über die "Treiber"-
bzw. "Anwendungen & Aktualisierungen"-Anwendung bei Ubuntu-Derivaten möglich.

## Compact Disks

1.	Replace deleted bytes with zeroes in the virtual machine.

	```bash
	apt install zerofree
	zerofree -v /dev/sda1
	```

2.	Compact zeroed disks on the host.

	```bash
	vboxmanage modifyhd --compact Finroc/Finroc.vdi
	```

	The `modifyhd` command supports file names and UUIDs.

	```bash
	vboxmanage modifyhd --compact XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
	```
