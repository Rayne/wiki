# Linux

## Arbeitsspeicher

```bash
lshw -short -C memory
```

```
H/W-Pfad              Gerät           Klasse      Beschreibung
===============================================================
/0/0                                   memory      64KiB BIOS
/0/28                                  memory      16GiB Systemspeicher
/0/28/0                                memory      Project-Id-Version: lshwRepor
/0/28/1                                memory      16GiB DIMM DDR4 Synchron Unbu
/0/28/2                                memory      Project-Id-Version: lshwRepor
/0/28/3                                memory      Project-Id-Version: lshwRepor
/0/2a                                  memory      576KiB L1 Cache
/0/2b                                  memory      3MiB L2 Cache
/0/2c                                  memory      16MiB L3 Cache
```

## CPU-Kerne

**Aktive Kerne**

```
grep "cpu core" /proc/cpuinfo | wc -l
```

**Kerne aktivieren**

```
for i in {1..11}; do echo 1 > /sys/devices/system/cpu/cpu"$i"/online; done
```

**Kerne deaktivieren**

```
for i in {1..11}; do echo 0 > /sys/devices/system/cpu/cpu"$i"/online; done
```

*Der erste Kern (`cpu0`) kann nicht deaktiviert werden.*
