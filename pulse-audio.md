# Pulse Audio

## Noise in the Audio Signal

When "metallic noise" appears in the audio output, replace the running PulseAudio daemon with a new one.

```bash
pulseaudio --kill
```

## Microphone records only Noise

- Disable unused devices to narrow down the issue
- Disable duplex input and output for audio output

## Microphone Input with Acoustic Echo Cancellation

Add

```
load-module module-echo-cancel
```

or

```
load-module module-echo-cancel source_name=FilteredMicrophone source_properties=device.description=FilteredMicrophone
```

at the end of `/etc/pulse/default.pa`.
Run `pulseaudio -k` as user or reboot the system.

### Test

It is possible to load modules on the fly and without persisting these changes, e.g.

```bash
pactl load-module module-echo-cancel source_name=FilteredMicrophone source_properties=device.description=FilteredMicrophone
```

returns a number representing the newly instantiated module.
The resulting device can be removed with

```bash
pactl unload-module 31
```

where `31` is the number returned by `pactl load-module`.

### References

- [Documentation of `module-echo-cancel`](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/#index45h3)
- [Excellent answer on askubuntu.com](https://askubuntu.com/a/765024)
- [Examples in the Arch Linux Wiki](https://wiki.archlinux.org/index.php/PulseAudio/Examples)
- `pactl list`
