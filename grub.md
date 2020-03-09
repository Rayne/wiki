# GRUB

## Reboot to specific GRUB entry

```bash
sudo grub-reboot 4
xfce4-session-logout --reboot
```

Alternativ:

```bash
# @see /boot/grub/grub.cfg 
grub-reboot "Windows 10 (auf /dev/sdc1)"
```
