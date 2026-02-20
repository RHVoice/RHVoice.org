---
title: "Using RHVoice on Linux"
---

There are three possible options of installing RHVoice on Linux:

1. An up-to-date package distributed through the Snap Store. Below we describe how to install it.
2. One of the packages built for specific Linux distributions. Not all of them will be up-to-date and provide all the voices. See [this page](https://github.com/RHVoice/RHVoice/blob/master/doc/en/Packaging-status.md) for more information.
3. Compiling from source: visit [RHVoice source repository](https://github.com/RHVoice/RHVoice) to learn more.

Distribution through the Snap packaging system is preferred by the developers of the core RHVoice engine, as it allows us to easily publish a single up-to-date binary. If you are not familiar with snaps, please visit [this website](https://snapcraft.io/) to learn about them. Your preferred Linux distribution may already have this system preinstalled, or it may be available as a package in its repository.

## Install RHVoice snap

The snap only installs the RHVoice TTS engine itself, including the module connecting RHVoice to Speech Dispatcher. Voices need to be installed via the newly implemented built-in command-line voice manager.

Most of the commands described below need to be run as root. We will assume you use the sudo command.

To install the snap, run this command:
```
sudo snap install rhvoice
```

Now you need to install a voice. The voice manager must be run as root. In theory some of its commands shouldn't require it, but we haven't implemented such functionality yet.

To list available voices, run:
```
sudo rhvoice.vm -a
```

Let's assume we would like to install the English voice called Alan:
```
sudo rhvoice.vm -i alan
```

To list installed voices, run:
```
sudo rhvoice.vm -l
```

Now let's test if it speaks:
```
echo hello|rhvoice.test
```

## Use RHVoice with Orca

If you use the Orca screen reader, you will need to manually connect RHVoice to Speech Dispatcher, which is the software Orca relies on to work with TTS engines. Unfortunately, we are not aware of any way we could register RHVoice with Speech Dispatcher automatically.

Orca is the default screen reader in Linux distributions such as Ubuntu, Fedora and Debian. The method described below has been tested on Ubuntu. If it doesn't work on your Linux distribution, please let us know.

1. Install the RHVoice snap and at least one voice as explained in the previous section.
2. Open the terminal and change to the directory that contains the Speech Dispatcher modules:
```
cd /usr/lib/speech-dispatcher-modules
```
3. Create a symbolic link to RHVoice's module for Speech Dispatcher:
```
sudo ln -s /snap/rhvoice/current/bin/sd_rhvoice
```
3. Reboot. You should now be able to select RHVoice and your favorite voice in Orca.
