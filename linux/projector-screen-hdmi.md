

## List all device

```bash
xrandr
```

## Export to device

```bash
xrandr --output <device-name> --auto
```

Example:

```bash
xrandr --output HDMI-2 --auto
```


## Only the second screen
```bash
xrandr --output HDMI-2 --auto --output eDP-1 --off
```
