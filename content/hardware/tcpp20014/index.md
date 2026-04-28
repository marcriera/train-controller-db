---
title: "Ryojōhen controller (Sony PlayStation 2)"
hidden: true
---

{{% hardware-overview tcpp20014 %}}
{{% hardware-support tcpp20014 %}}

## Technical details

This controller has 2 handles (4 power notches and an analogue brake handle with three areas), a D-Pad and 7 buttons (Select, Start, Horn, Announce, Camera, Left doors, Right doors). In addition, it provides a 3.5 mm jack connector to plug a horn pedal.

Internally, it is a vendor-specific class device. The input data is compatible with HID, but the device does not provide a HID descriptor.

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | TAITO_DENSYA_CON_T03                      |
| **Manufacturer**            | TAITO                                     |
| **Vendor ID**               | 0x0AE4                                    |
| **Product ID**              | 0x0007                                    |
| **Serial number**           | TCPP20014                                 |
| **USB standard descriptor** | [Download](standard-descriptor.txt) |
| **HID report descriptor**   | [Download](hid-report-descriptor.txt) (recreated, not provided by actual device) |

### Input

The controller sends reports to the host (PS2) formed by 8 bytes:

| Byte # | Data            |
|:------:|:---------------:|
| 1      | Brake           |
| 2      | Power           |
| 3      | Pedal           |
| 4      | D-Pad           |
| 5      | Buttons         |
| 6      | *Unused*        |
| 7      | *Unused*        |
| 8      | *Unused*        |

Unlike traditional controllers, the brake handle is analogue and the brake byte reflects the position of the handle precisely. There are three areas with the ranges listed below, plus the emergency notch.

| Position          | Range     |
|:-----------------:|:---------:|
| Reduce pressure   | 0x23-0x64 |
| Keep pressure     | 0x65-0x89 |
| Increase pressure | 0x8A-0xD6 |
| Emergency         | 0xD7      |

When using the controller with **Densha de GO! Professional 2** or **Densha de GO! Final**, the brake handle is interpreted as having 6 brake notches + emergency. The aproximate byte range for each notch is listed below (taken from **Densha de GO! Professional 2**).

| Notch     | Range     |
|:---------:|:---------:|
| Released  | 0x23-0x2A |
| B1        | 0x2B-0x3C |
| B2        | 0x3D-0x4E |
| B3        | 0x4F-0x63 |
| B4        | 0x64-0x8A |
| B5        | 0x8B-0xB0 |
| B6        | 0xB1-0xD6 |
| Emergency | 0xD7      |

The values for the power notch byte are the following. Between notches, a transition value of **0xFF** is reported.

| Notch      | Value |
|:----------:|:-----:|
| N          | 0x00  |
| P1         | 0x3C  |
| P2         | 0x78  |
| P3         | 0xB4  |
| P4         | 0xF0  |

The pedal byte has two possible values depending on the state of the pedal.

| State      | Value |
|:----------:|:-----:|
| Released   | 0xFF  |
| Pressed    | 0x00  |

The D-pad byte represents the input from the **Up**, **Down**, **Left** and **Right** physical buttons. If two opposite directions are pressed simultaneously, the result is **None** unless a third button is pressed.

| Button     | Value       |
|:----------:|:-----------:|
| Up         | 0x00        |
| Up+Right   | 0x01        |
| Right      | 0x02        |
| Down+Right | 0x03        |
| Down       | 0x04        |
| Down+Left  | 0x05        |
| Left       | 0x06        |
| Up+Left    | 0x07        |
| None       | 0x08        |

The button byte uses bits to represent the state of the physical buttons. **0** means that the button is released and **1** that it is pressed.

| Bit | Physical Button |
|:---:|:---------------:|
| 1   | Horn            |
| 2   | Announce        |
| 3   | Camera          |
| 4   | Right doors     |
| 5   | Left doors      |
| 6   | Select          |
| 7   | Start           |
| 8   | *Unused*        |
