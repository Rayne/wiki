# Microsoft Windows

## Herunterfahren

Umschalttaste beim "Herunterfahren" gedrückt halten,
damit "richtig" heruntergefahren wird
(z.B. Nutzer vollständig abmelden und Laufwerke aushängen).

Another solution:

```
shutdown /s /t 0
```

For convenience, a shortcut (e.g. on the desktop) can be created to execute this snippet.

## Self-Repair Failure

The following sections provide possible solutions to fix a Windows installation that is rebooting immediately when trying to repair itself.

⚠️ _All suggested fixes may damage the Windows installation._

### Make read-only NTFS partition writable

- **Problem**: When the Windows partition is marked as ready-only, Windows may fail to repair itself.

  **Experiment**: Remove the read-only flag from the Windows partition.

  1. Boot a Windows installation medium (or "Reparaturmodus"/"Abgesicherter Modus" from the current installation)

     _**TODO** How does one enter the integrated repair mode?_

  1. Select repair options

  1. Try automatic repair (which will certainly fail)

  1. Select the command line option

  1. Execute `diskpart`

  1. Enter `list volume`

  1. Assuming Windows is installed on volume 2 and mounted with letter `D`: `select volume 2`

  1. Remove read-only flag with `attributes disk clear readonly`

  1. `quit`

  1. `chkdsk /f D:` for good measure.
     The program may report that the volume is in good shape and there is nothing to fix

  1. `exit`

  1. Reboot into the installed system

  1. Windows may now be able to "fix" the no longer read-only volume

### Force NTFS-3G to mount a hibernated volume in write-mode

A hibernated volume can only be mounted in read-only mode.
In most cases, this is the correct solution.
If one needs to write to a hibernated volume (or one that looks like a hibernated volume), the hibernation information can be forcefully removed.

```bash
mount -o remove_hiberfile /dev/sdc1 /media/tmp/
```
