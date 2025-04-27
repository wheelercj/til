+++
title = 'Setting up Solaar for Ubuntu'
date = 2024-11-04T22:37:04-08:00
lastmod = 2024-12-18T16:40:59-08:00
+++

I'm switching from Windows 11 to Ubuntu 22.04.5 LTS, and my mouse's (Logitech MX Vertical) official software for rebinding buttons isn't supported. That's why I'm using [Solaar](https://github.com/pwr-Solaar/Solaar?tab=readme-ov-file) to rebind the mouse buttons. It's a little confusing to set up.

First, install Solaar with these commands:

```shell
sudo apt update
sudo apt install solaar
```

At least for Ubuntu 22.04.5 LTS with Wayland, don't install using the PPA because it results in various errors like these:

```shell
$ solaar --version
rules cannot access modifier keys in Wayland, accessing process only works on GNOME with Solaar Gnome extension installed
cannot create uinput device: "/dev/uinput" cannot be opened for writing
solaar 1.1.13
```

(I later changed from Wayland to X11 for other reasons, but the instructions here still work.)

Following the instructions above, you should get output like this:

```shell
$ solaar --version
solaar 1.1.1
```

Then open Solaar's GUI. It should find your mouse automatically and list it on the left side of the window. Maybe try reconnecting the mouse if it doesn't.

I wanted to rebind my mouse's back and forwards buttons to switch to the previous tab and previous window, respectively. To do this, I had to find the options titled "Key/Button Diversion" in the main menu, unlock them, and set "Back Button" and "Forward Button" each to "Diverted". This allows Solaar to intercept events from the mouse, but doesn't tell Solaar what to do with them yet.

Next, I had to open Solaar's rule editor and, in the "User-defined rules" section, create a new rule with two sub-rules. The first sub-rule had to have a key condition set to "Back Button" and a key press action set to "Control_L" and "Tab". The second sub-rule was the same but with the "Forward Button" key condition and the "Alt_L" and "Tab" key press action.

After saving the changes, I can now switch windows and tabs with my extra mouse buttons!

While figuring this out, discussions online mentioned that figuring out which key names to use can be difficult, and manufacturers often design mice in ways that are inconsistent and/or cause compatibility problems. Unfortunately, a lot of it may be trial and error sometimes. If Solaar doesn't work for you, there are other options out there, though I don't really know anything about them.

## Further reading

- [Solaar is a Linux manager for many Logitech keyboards, mice, and other devices \| Hacker News](https://news.ycombinator.com/item?id=42454359)
- [Solaar | Linux device manager for Logitech devices](https://pwr-solaar.github.io/Solaar/)
- [Solaar GUI Usage | Solaar](https://pwr-solaar.github.io/Solaar/usage)
- [Rule Processing of HID++ Notifications | Solaar](https://pwr-solaar.github.io/Solaar/rules)
