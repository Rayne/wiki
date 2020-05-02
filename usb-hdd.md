# USB-HDD

```bash
udisksctl power-off -b /dev/sda
```

## EXT

### Lazy Initialization

Test mit einer LUKS-verschlüsselten Seagate Expansion+ 4 TB-Festplatte via USB
und mit SMR-Technik.

-	Lazy Initialization erledigt einen Großteil der notwendigen Arbeit während das Block-Device produktiv benutzt werden kann.
	Die Schreibgeschwindigkeit der späteren
	[Initialisierung liegt bei max. 16MB/s](https://www.thomas-krenn.com/en/wiki/Ext4_Filesystem#Lazy_Initialization)
	und dauert daher je nach Größe des Geräts länger.
	Der Vorgang kann jederzeit (automatisch) unterbrochen werden,
	z.B. wenn eine Festplatte entfernt werden soll.

	```bash
	time mkfs.ext4 -m 0 -L "$mappername" "/dev/mapper/$mappername"
	[…]
	Ein Dateisystem mit 976754133 (4k) Blöcken und 244195328 Inodes wird erzeugt.
	[…]
	Superblock-Sicherungskopien gespeichert in den Blöcken: 
		32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
		4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968, 
		102400000, 214990848, 512000000, 550731776, 644972544
	[…]
	real	0m24,645s
	user	0m0,047s
	sys	0m3,419s
	```

-	Die Initialisierung kann auch während der Formatierung
	und dabei mit maximaler Geschwindigkeit ausgeführt werden.
	Bei einem Test mit einer externen USB-SMR-HDD (Seagate Expansion+ 4 TB)
	dauerte die Initialisierung ca. 15 Minuten (vs. ca. 30 Sekunden).
	Die Schreibgeschwindigkeit pendelte zwischen 45MB/s und 120MB/s.
	Im Durchschnitt wurden ca. 75MB/s erreicht.

	```bash
	time mkfs.ext4 -m 0 -L "$mappername" -E lazy_itable_init=0,lazy_journal_init=0 "/dev/mapper/$mappername"
	[…]
	real	14m45,241s
	user	0m1,126s
	sys	1m14,597s
	```
