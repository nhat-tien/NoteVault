
As of 16.04, things become a lot simpler :)

Just install qjackctl and pulseaudio-module-jack module:

```bash
apt-get install qjackctl pulseaudio-module-jack
```

Then configure qjackctl to run the following command after startup. Copy it into "Setup..." > "Options" > "Execute script after Startup":

```
pactl load-module module-jack-sink channels=2; pactl load-module module-jack-source; pacmd set-default-sink jack_out
```

And that's it. Pulseaudio will recognize (through D-Bus) that JACK started, and automatically will route audio to it. When JACK is stopped Pulseaudio will revert to normal routing and start sending audio directly to card again.

So (almost) by default Pulseaudio implements the setup detailed above by mmv-ru.

## Ref 
https://askubuntu.com/questions/572120/how-to-use-jack-and-pulseaudio-alsa-at-the-same-time-on-the-same-audio-device
