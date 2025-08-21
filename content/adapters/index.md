---
title: "Adapters, tools and hacks"
weight: 3
---

Besides official compatibility, it is possible to use unofficial adapters, tools and hacks to use controllers with software which does not normally support train controllers.

## Autotraintas's DenConv tool {#autotraintas}

Autotraintas has created a tool that makes it possible to use nearly any Densha de GO! controller with the PC versions of the games. This includes classic console controllers (USB adapter required) and USB controllers. The tool patches the game memory on the fly to reflect the input from the controller.

The tool is available on their website: https://autotraintas.hariko.com


## Input plugins for BVE Trainsim/OpenBVE {#bve-plugin}

BVE Trainsim and OpenBVE both support **input plugins**, which allow expanding the controllers compatible with the software.

BVE Trainsim requires installing external input plugins, depending on the controller:

- [Console controllers](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (電GO PS - JC_PS101Uインターフェイス/電GO PS - JC_PS201Uインターフェイス by saha209, USB adapter required)
- [DGC-255/DGOC-44U/DRC-184](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (電GO PCインターフェイス by saha209)
- [TCPP-20009/TCPP-20014/MTC with P5/B8 cartridge](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (電GO PS2インターフェイス by saha209)
- [MTC (other cartridges)](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (TrainSimulator PS2 MultiTrainController(MTC)インターフェイス by saha209)
- [ZKNS-001](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (電GO SWインターフェイス by saha209)
- [OHC-PC01](http://www.konkyu.net/SanYingControllerInterface.aspx)

OpenBVE includes built-in input plugins supporting a wide range of controllers. They can be enabled and configured in the software settings.


## Sony PlayStation 2 cheat codes {#ps2-cheats}

While **Densha de GO! 3** and **Densha de GO! Shinkansen** officially support the original (non-USB) PlayStation controllers, the rest of PS2 software is only compatible with USB controllers. Via cheat codes, it is possible to use the original PlayStation controllers on real hardware, either with retail discs or via Open PS2 Loader.

The codes emulate a Type 2 controller. You will need to connect the controller as follows:

- Port 1: Dualshock or Dualshock 2 (D-pad, **SELECT**)
- Port 2: PlayStation controller (handles and buttons, **SELECT** is mapped to **D**)

{{% notice note %}}
Other controllers may be used like this with an adapter (Titan One/Titan Two + Brook adapter/PADEMU). In this case, buttons are not remapped and the Dualshock on port 1 is not needed. [More information](https://github.com/MarcRiera/ddgo-scripts/tree/main/Densha%20de%20GO!%20(PS1-PS2))
{{% /notice %}}

Each game requires a specific cheat code:

- [Densha de GO! Ryojōhen](ps2-cheats-tech/controller-cheat_ryojouhen.txt)
- [Densha de GO! Professional 2](ps2-cheats-tech/controller-cheat_pro2.txt)
- [Densha de GO! Professional 2 (TAITO Best)](ps2-cheats-tech/controller-cheat_pro2best.txt)
- [Densha de GO! Final](ps2-cheats-tech/controller-cheat_final.txt)

There are also cheat codes available for games in the **Train Simulator** series, emulating a Multi Train Controller (MTC):

- [Train Simulator: Midōsuji Line](ps2-cheats-tech/controller-cheat_midosuji.txt)
- [Train Simulator + Densha de GO!](ps2-cheats-tech/controller-cheat_tsddgo.txt)

For retail discs, the codes can be loaded with [ps2rd](https://github.com/mlafeldt/ps2rd) or [Cheat Device](https://github.com/root670/CheatDevicePS2). If you are using Open PS2 Loader, it already includes ps2rd and you just need to copy the codes and enable cheats.

Check the [technical description](ps2-cheats-tech) for all the details on how these cheat codes work. 


## USB adapters

Console controllers can be used with many software using a USB adapter. While there is a wide variety of adapters in the market at all prices, not every one is supported. Check for the following when looking for a USB adapter:

1. Make sure the adapter converts every button independently and does not combine four of them into a D-pad. The Sony PlayStation and Nintendo 64 controllers require pressing button combinations not possible on a D-pad and data may be incorrect. This can lead to erratic behaviour (handles moving in unexpected ways).
2. Make sure the software you want to use the adapter with supports the adapter. Most software support any adapter and allow calibration (button mapping), but a few only support very specific models.


## Titan One/Titan Two adapters {#adapter-titan}

[ConsoleTuner](https://www.consoletuner.com) sells the Titan One and Titan Two USB devices. They support scripts to remap buttons or change the behaviour of a controller entirely. There are many repositories available with scripts to make a *Densha de GO!* controller behave like a different one:

- [tylau0/DenGo](https://github.com/tylau0/DenGo)
- [arnauos/densha-de-go](https://github.com/arnauos/densha-de-go)
- [mikaeltarquin/densha-de-go](https://github.com/mikaeltarquin/densha-de-go)
- [thmalex/DenshaDeGoPS1toPS4](https://github.com/thmalex/DenshaDeGoPS1toPS4)
- [MarcRiera/ddgo-scripts](https://github.com/MarcRiera/ddgo-scripts)

Before using a script, check whether it was designed for the Titan One or the Titan Two. Scripts all use the same extension (.GPC) but are different. The Titan Two is backwards compatible with many Titan One scripts, but not viceversa.
