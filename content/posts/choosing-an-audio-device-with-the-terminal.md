+++
title = 'Choosing an audio device with the terminal'
date = 2024-12-22T18:00:52-08:00
lastmod = 2024-12-22T23:03:19-08:00
+++

I often switch between using speakers and headphones. My Ubuntu laptop sometimes automatically switches to the correct device when I plug in or unplug headphones like it's supposed to. However, for some reason it sometimes chooses an option that cannot play audio: `HDMI / DisplayPort 2 Output - Renoir Radeon High Definition Audio Controller`.

I got tired of opening settings, navigating to audio, and changing the output device, so I decided to look into ways to make this easier. Searching online led me to [sound - How can I change the default audio device from command line? - Ask Ubuntu](https://askubuntu.com/questions/14077/how-can-i-change-the-default-audio-device-from-command-line) which says to use a tool called `pacmd` that appears to be installed by default in Ubuntu.

With some reading and experimentation, I found that this command switches to the correct audio device:

```bash
pacmd set-default-sink 3
```

The `3` is the `index` of the audio device listed with `pacmd list-sinks`. "Sink" is a category of audio devices that includes speakers, and "source" includes microphones. Data travels from sources and to sinks within the computer.

The `pacmd list-sinks` command has a lot of output, but you only need to look at the values of the `device.description` properties to find the right one.

With that information, I created a custom command by adding to my `~/.bashrc`:

```bash
alias ,fix-audio="pacmd set-default-sink 3"
```

To test this, I switched to the incorrect audio device in settings while music was playing, and then ran my new `,fix-audio` command. Starting its name with a comma was inspired by [Start all of your commands with a comma](https://rhodesmill.org/brandon/2009/commands-with-comma/).

I was hoping to somehow prevent the incorrect audio choice from ever being automatically chosen, and maybe I will find a way to do that someday, but at least fixing the audio is easier now.
