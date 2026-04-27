---
title: "Multi Train Controller (Sony PlayStation 2)"
hidden: true
---

{{% hardware-overview sotp031201 %}}
{{% hardware-support sotp031201 %}}

## Technical details

This controller has one handle with several notch cartridges (P4/B7, P4/B2-B7, P5/B5, P5/B7, B5/B8, P13/B7), a D-Pad and 7 buttons (Select, Start, A, B, C, D, ATS). The A button can distinguish between "soft" and "hard" presses. In addition, the controller has four lamps.

Internally, it is a vendor-specific class device. The input data is compatible with HID, but the device does not provide a HID descriptor. The USB descriptors and the reported data change depending on the notch cartridge inserted. 

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | *None*                                    |
| **Manufacturer**            | *None*                                    |
| **Vendor ID**               | 0x0AE4<br>0x1C06 (P5/B5)                  |
| **Product ID**              | 0x0101<br>0x77A7 (P5/B5)<br>0x0004 (P5/B8) |
| **Serial number**           | *None*                                    |
| **USB standard descriptor** | [P4/B7](P4B7_standard-descriptor.txt)<br>[P4/B7 (without B1)](P4B1B7_standard-descriptor.txt)<br>[P5/B5](P5B5_standard-descriptor.txt)<br>[P5/B7](P5B7_standard-descriptor.txt)<br>[P5/B8](P5B8_standard-descriptor.txt)<br>[P13/B7](P13B7_standard-descriptor.txt) |
| **HID report descriptor**   | [P4/B7, P4/B2-B7, P5/B7, P13/B7](hid-report-descriptor.txt) (recreated, not provided by actual device) |

### P5/B5 cartridge

When this cartridge is inserted, the controller emulates the [Train Mascon]({{% relref cotm02001 %}}). The buttons are mapped 1:1 except the **D** button, which is mapped to the **Close** (**閉**) button.

The lamps are used as follows, from top to bottom: doors, ATS, 45 and 15.

### P5/B8 cartridge

When this cartridge is inserted, the controller emulates the [Two handle controller "Type 2"]({{% relref tcpp20009 %}}). The buttons are mapped 1:1 and **ATS** is mapped to **START**. The reverser is mapped to the D-pad **UP** and **DOWN** buttons.

Only the top lamp is used, for the doors.

### P4/B7, P4/B2-B7, P5/B7, P13/B7 cartridges

When any of these cartridges is inserted, the controller functions similarly to the P5/B5 mode and data changes depending on the amount of notches. The specific cartridge in use can be detected by looking at the *bcdDevice* value from the standard USB descriptor:

| Cartridge | bcdDevice |
|:---------:|:---------:|
| P4/B7     | 0x0300    |
| P4/B2-B7  | 0x0400    |
| P5/B7     | 0x0800    |
| P13/B7    | 0x0A00    |

#### Input

The controller sends reports to the host (PS2) formed by 4 bytes:

| Byte # | Data            |
|:------:|:---------------:|
| 1      | 0x01 (*fixed*)  |
| 2      | Reverser+handle |
| 3      | Buttons 1       |
| 4      | Buttons 2       |

The reverser+handle byte combines two values representing the state of the reverser and the power/brake handle. The handle notch is represented sequentially starting from **0x1** (Emergency), brake notches from highest to lowest, *N* and power notches from lowest to highest.

| Position   | Value |
|:----------:|:-----:|
| Forward    | 0x8X  |
| Neutral    | 0x0X  |
| Backward   | 0x4X  |

{{% notice note %}}
The P5/B7 and P13/B7 cartridges do not make use of the reverser and use both nibbles for the handle notch.
{{% /notice %}}

The first button byte uses bits to represent the state of the physical buttons. **0** means that the button is released and **1** that it is pressed.

| Bit | Physical Button |
|:---:|:---------------:|
| 1   | ATS             |
| 2   | D               |
| 3   | A (soft)        |
| 4   | A (hard)        |
| 5   | B               |
| 6   | C               |
| 7   | *Unused*        |
| 8   | *Unused*        |

The second button byte also uses bits to represent the state of the physical buttons.

| Bit | Physical Button |
|:---:|:---------------:|
| 1   | Start           |
| 2   | Select          |
| 3   | Up              |
| 4   | Down            |
| 5   | Left            |
| 6   | Right           |
| 7   | *Unused*        |
| 8   | *Unused*        |

#### Output

The controller supports receiving data via a control transfer to turn on/off the lamps. The setup packet is as follows:

| Data          | Value       |
|:-------------:|:-----------:|
| bmRequestType | 0x40        |
| bRequest      | 0x50        |
| wValue        | *Lamp data* |
| wIndex        | 0x0         |
| wLength       | 0x0         |

Changing *wValue* controls the lamps with the logic below.

* **Door lamp:** **0x0X** is **Off**, **0x1X** is **On**.
* **Signal lamp:** **0xX0** is **Off**, **0xX1** is **ATS**, **0xX2** is **45**, **0xX3** is **15**.
