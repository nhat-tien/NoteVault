+++
title = "Fix Microphone Noise Background on Ubuntu"
date = "2024-03-26"
lastmod = "2025-08-24"
draft = false
tags = [ "linux", "fix" ]
+++

## Update

Just use NoiseTorch, the best solution.

- [https://github.com/noisetorch/NoiseTorch](https://github.com/noisetorch/NoiseTorch)

Ignore the solution below

## Solution

- Add below script to `/etc/pulse/default.pa`

```txt
load-module module-echo-cancel source_name=noechosource sink_name=noechosink
set-default-source noechosource
set-default-sink noechosink
```

> the `noechosource` and `noechosink` are just name, you can rename it to whatever you want

- Reload pulseAudio by `pulseaudio -k` 
- Choose new device in settings of pulseAudio

## Ref
- [https://askubuntu.com/questions/18958/realtime-noise-removal-with-pulseaudio](https://askubuntu.com/questions/18958/realtime-noise-removal-with-pulseaudio)
- [https://www.youtube.com/watch?v=UNhJCD9H8Uw](https://www.youtube.com/watch?v=UNhJCD9H8Uw)
