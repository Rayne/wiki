# Linux

## Memory

```bash
lshw -short -C memory
```

```text
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

## CPU

- `lscpu` reads `/proc/cpuinfo`

- Active CPU cores

  ```bash
  grep "cpu core" /proc/cpuinfo | wc -l
  ```

- Enable CPU cores

  ```bash
  for i in {1..11}; do echo 1 > /sys/devices/system/cpu/cpu"$i"/online; done
  ```

- Disable CPU cores

  ```bash
  for i in {1..11}; do echo 0 > /sys/devices/system/cpu/cpu"$i"/online; done
  ```

  *The first core (`cpu0`) can't be disabled.*

### CPU Frequency

- Current frequency

  ```bash
  watch -n0 'lscpu | grep MHz | tr -d " " | cut -d : -f 2'
  ```

- Frequency range

  ```bash
  echo "[$(cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_min_freq), $(cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_max_freq)]"
  ```

- Limit the frequency range

  ```bash
  max_freq=800000

  for f in /sys/devices/system/cpu/cpu*/cpufreq/scaling_max_freq; do echo -n "$max_freq" > "$f"; done
  ```
