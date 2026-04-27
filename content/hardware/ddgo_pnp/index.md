---
title: "Densha de GO! Plug and Play"
hidden: true
---
{{% hardware-overview ddgo_pnp %}}
{{% hardware-support ddgo_pnp %}}

## Technical details

This controller is a self-contained console with a modified version of *Densha de GO! Final*. Externally, it looks similar to a TCPP-20009, except it does not include a pedal connection. It requires a micro USB cable for power and a HDMI cable for video output.

Internally, it contains an Allwinner R16-based board running a Linux distro. The micro USB port supports USB OTG with a powered adapter and is used by Taito to install software updates. Full details are available on [Linux Sunxi Wiki](https://linux-sunxi.org/index.php?title=TAITO_Densha_de_GO!_Plug_%26_Play).

## Mods

There are several unofficial mods available to improve or add functionality to the console:

| **Mod**                     | **Site**                                                               | **Description**                                                                                         |
|-----------------------------|------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| Chime Patcher               | [Link](https://github.com/GMMan/dengo-plug-and-play-chimes-patch)      | Restores the station jingles and musical horns from *Densha de GO! Final*.                              |
| Controller mod              | [Link](https://github.com/MarcRiera/ddgo-pnp-controller)               | Allows using the console as a USB controller for PC and consoles. Several controller models available.  |
| Controller mod (legacy)     | [Link](https://github.com/GMMan/dengo-plug-and-play-controller)        | Allows using the console as a DGOC-44U controller. Superseded by the newer multi-controller mod.        |
| Overclock script            | [Link](https://gist.github.com/GMMan/5b5daa43d7922d1e32a1b79cf344ad01) | Sets the console's CPU to a higher (but safe) clock rate to improve performance. **May cause crashes.** |
| Translation Patcher         | [Link](https://github.com/zapan/dengo-plug-and-play-translation-patch) | English translation for *Densha de Go! Plug & Play*.                                                    |

## Recovery bootloader

A [recovery bootloader](https://git.marcriera.cat/marc/ddgo-pnp-recovery-uboot) allowing full access to the internal MMC storage for backups/restore is available. It is based on mainline U-Boot.
