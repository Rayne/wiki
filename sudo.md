# sudo

## Login-Shell

```bash
sudo -i
```

## Ohne Passwort

```bash
visudo -f /etc/sudoers.d/dennis
```

```
dennis ALL=(ALL) NOPASSWD: …/dennis-amd-rx-470-slowdown
```

## Pro-Tipps

> A common pilot error on sudo based systems is to forget the sudo prefix on a command that requires extra privileges.
> A novice retypes the whole command.
> The diligent student edits the command from the shell's command history.
> The enlightened one types sudo !!.
>
> -- https://unix.stackexchange.com/a/3748/10938
