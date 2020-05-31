# ZFS-Experimente

```
apt install zfsutils-linux
```

```
lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0    7:0    0 89,1M  1 loop /snap/core/7917
loop1    7:1    0 54,7M  1 loop /snap/lxd/12211
sda      8:0    0   32G  0 disk 
├─sda1   8:1    0    1M  0 part 
└─sda2   8:2    0   32G  0 part /
sdb      8:16   0   10G  0 disk 
sdc      8:32   0   10G  0 disk 
sdd      8:48   0   10G  0 disk 
sr0     11:0    1 1024M  0 rom
```

Die Pools sollen das Alignment der Festplatte nutzen,
d.h. 4kB-Blöcke.
Wir benötigen somit das Argument `ashift=12`, da`2^12 = 4096`.

```
zpool create -o ashift=12 mypool /dev/sdb
```

```
lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0    7:0    0 89,1M  1 loop /snap/core/7917
loop1    7:1    0 54,7M  1 loop /snap/lxd/12211
sda      8:0    0   32G  0 disk 
├─sda1   8:1    0    1M  0 part 
└─sda2   8:2    0   32G  0 part /
sdb      8:16   0   10G  0 disk 
├─sdb1   8:17   0   10G  0 part 
└─sdb9   8:25   0    8M  0 part 
sdc      8:32   0   10G  0 disk 
sdd      8:48   0   10G  0 disk 
sr0     11:0    1 1024M  0 rom
```

## Pool vergrößern - Redundanz

```
zpool attach mypool /dev/sdb /dev/sdc
zpool status
```

```
zpool status
```

```
  pool: mypool
 state: ONLINE
  scan: resilvered 1,14M in 0 days 00:00:00 with 0 errors on Wed Oct 30 13:58:38 2019
config:

	NAME        STATE     READ WRITE CKSUM
	mypool      ONLINE       0     0     0
	  mirror-0  ONLINE       0     0     0
	    sdb     ONLINE       0     0     0
	    sdc     ONLINE       0     0     0

errors: No known data errors
```

```
zpool list 
```

```
NAME     SIZE  ALLOC   FREE  CKPOINT  EXPANDSZ   FRAG    CAP  DEDUP    HEALTH  ALTROOT
mypool  9,50G   696K  9,50G        -         -     0%     0%  1.00x    ONLINE  -
```

## Kompression aktivieren

Der Kompressionsgrad kann jederzeit geändert werden.
Die Einstellung betrifft aber nur neue Daten.
Alte Daten werden nicht aktualisiert.

```
zfs set compression=lz4 mypool 
```

## Dateisysteme und Snapshots

Da man die "Wurzel" nicht nutzen soll für Dateien,
legen wir ein neues System an.

```
zfs create mypool/testarea
cd /mypool/testarea
```

> Darüber hinaus ist es nicht ratsam, Dateien in diesem Wurzel-Dateisystem anzulegen. Man bewahrt sich viel mehr Flexibilität, wenn man dieses eine leer lässt. In diesem Beispiel wird deswegen ein Dateisystem erzeugt, in dem tatsächlich auch einmal etwas gespeichert werden wird:
>
> -- https://wiki.ubuntuusers.de/ZFS_on_Linux

```
cd /mypool/testarea
echo "Test A" > fileA

zfs snap mypool/testarea@fileA
zfs list -t snap

rm fileA

zfs rollback mypool/testarea@fileA

zfs clone mypool/testarea@fileA mypool/clone
```

**Snapshots anschauen**

Snapshots werden automatisch als Read-Only eingehängt,
wenn man in das "fehlende" (nicht nur versteckte) Verzeichnis `.zfs` wechselt.

```
cd /mypool/testarea/.zfs
```

## Snapshots sichern

Siehe [send/recv](https://wiki.ubuntuusers.de/ZFS_on_Linux/#send-recv).

-	Vollständige Sicherung

	```
	## Bei der hier vorgeführten Methode muss das Zieldateisystem bereits vorhanden sein
	zfs create mypool/receivedemo
	zfs send -R mypool/testarea@file1-5.txt-erzeugt | zfs recv -F mypool/receivedemo
	zfs list -t all 
	```

-	Inkrementelle Sicherung

	```
	zfs diff  mypool/testarea@file3.txt-geaendert 
	```

## Pool vergrößern - Speicherplatz

```
zpool add -f POOL DISK
```

## Zwei Mirrors in einem Schritt

```
zpool create mypool mirror /mnt/free-space/simulate.disk{1,3} mirror /mnt/free-space/simulate.disk{2,4}
```

## Status

```
zfs list
zpool list
zpool status
```

```
zfs get all mypool/testarea | awk '$3 ~ /[GEKMx]$/' 
```

```
NAME             PROPERTY              VALUE                 SOURCE
mypool/testarea  used                  1,62M                 -
mypool/testarea  available             9,20G                 -
mypool/testarea  referenced            1,62M                 -
mypool/testarea  compressratio         8.29x                 -
mypool/testarea  recordsize            128K                  default
mypool/testarea  usedbydataset         1,62M                 -
mypool/testarea  refcompressratio      8.29x                 -
mypool/testarea  written               1,62M                 -
mypool/testarea  logicalused           12,5M                 -
mypool/testarea  logicalreferenced     12,5M                 -
```

## Links

-	https://wiki.ubuntuusers.de/ZFS_on_Linux/#Beispiele
-	https://serverfault.com/a/31275/250668

	> Think about the filesystem, too. Your 4x 500GB example is about the largest capacity I would recommend with good conscience for ext3. I do not recommend to create much larger ext3 filesystems because e.g. fsck time can be enormous. Create several smaller instead of one large filesystem.
	> As you mentioned video data: ext3 handles large files inefficiently because it'll have to create indirect, double-indirect and triple-indirect metadata blocks to store the data of large files and you'll pay the price. Nowadays, ext4 supports extents and handles this much better. But then, it is rather new and e.g. Red Hat Enterprise Linux 5 does not support it yet. (Some Enterprise distros will support alternatives like XFS).
	> If there is data corruption on any data block you'll have a hard time to even notice this with Linux filesystems. ZFS on the other hand checksums all metadata and data and also verifies the checksum every time data is read from disk. (There is also background scrubbing)
	> RAID rebuild time on Linux is proportional to disk size because the RAID layer does not know the contents of the filesystem (layer). ZFS's RAID-Z rebuild time depends on the amount of actual data on the failed disk because only used blocks will be copied/rebuilt on a replacement disk.
	> Do you want to snapshot your filesystems? LVM snapshots don't even compare with ZFS's instantaneous snapshots. The latter can also easily exposed to the end-users e.g. for easy restores.
	> Use RAID6 (RAID-Z2) and not only RAID5 (RAID-Z) with large disks (>500GB) because chances are that another disk will fail during rebuilt.
