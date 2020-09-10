---
permalink: /pipewire
---
# PipeWire: Explainer and Installation Guide

## What's PipeWire?

[PipeWire](https://pipewire.org) is Red Hat's latest attempt at replacing and simplifying the Linux video and audio stack, mainly [ALSA](https://alsa-project.org), [JACK](https://jackaudio.org/), and [PulseAudio](https://pulseaudio.org), with the goal of being a drop-in replacement for all of them.

## Why care?

If you've ever interacted with audio (especially real-time or networked audio) on Linux, you've likely experienced headaches at one point or another. This is usually because Linux audio is heavily fragmented: PulseAudio this, ALSA that, JACK; you might have even heard OSS mentioned! Does this seem simple to you? Applications with sound on Linux are almost forced to have layers upon layers of hacks for legacy support. Enter PipeWire.

# How to install PipeWire and replace PulseAudio and JACK on your machine

***A warning:*** *PipeWire doesn't have 100% feature parity with PulseAudio or JACK yet. If you're a poweruser of PulseAudio's network features, for example, you might want to hold off on it for a while.*

With that out of the way, the process is relatively simple.

1. Use your package manager to grab PipeWire:

    sudo dnf install pipewire-libpulse pipewire-libjack pipewire-alsa

2. Replace PulseAudio and JACK Libraries with PipeWire's

```
    cd /usr/lib64/

    sudo ln -sf pipewire-0.3/pulse/libpulse-mainloop-glib.so.0 /usr/lib64/libpulse-mainloop-glib.so.0.999.0
    sudo ln -sf pipewire-0.3/pulse/libpulse-simple.so.0 /usr/lib64/libpulse-simple.so.0.999.0
    sudo ln -sf pipewire-0.3/pulse/libpulse.so.0 /usr/lib64/libpulse.so.0.999.0

    sudo ln -sf pipewire-0.3/jack/libjack.so.0 /usr/lib64/libjack.so.0.999.0
    sudo ln -sf pipewire-0.3/jack/libjacknet.so.0 /usr/lib64/libjacknet.so.0.999.0
    sudo ln -sf pipewire-0.3/jack/libjackserver.so.0 /usr/lib64/libjackserver.so.0.999.0

    sudo ldconfig
```

3. To verify PipeWire was installed successfully, run:

```
    pactl info | head -1
    # This should return:
    # Server String: pipewire-0
```

4. Reboot the system

Congratulations! You've successfully installed PipeWire. Enjoy!

If you encounter any bugs, you can report them [here](https://gitlab.freedesktop.org/pipewire/pipewire/-/issues).
