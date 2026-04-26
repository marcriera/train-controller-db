---
title: "ZUIKI Mascon Pro"
hidden: true
---

{{% hardware-overview zkns021 %}}
{{% hardware-support zkns021 %}}

## Technical details

This controller has a reverser handle (3 positions), a brake/power handle (5 power notches and 8+emergency brake notches) and 22 buttons, one with a lamp (**EB Reset**). A USB-A port at the back allows connecting a horn pedal with two active positions (light and strong). In addition, it provides a door lamp.

Internally, it is a HID-compliant joystick with 17 buttons, a hat switch and 4 axes.

Despite using a USB-A connector, the horn pedal port does not follow USB specifications. It merely exposes two electrical circuits for the two pedal positions.

|                             |                                       |
|-----------------------------|---------------------------------------|
| **Product name**            | ZUIKI MASCON PRO                      |
| **Manufacturer**            | *None*                                |
| **Vendor/Product ID**       | 0x33DD/0x0006                         |
| **Serial number**           | *None*                                |
| **USB standard descriptor** | [Download](standard-descriptor.txt)   |
| **HID report descriptor**   | [Download](hid-report-descriptor.txt) |

### Input

#### Buttons

The button data of the HID report represents input from most physical buttons. Each button in the HID report uses one bit. **0** means that the button is released and **1** that it is pressed.

| HID Button # | Physical Button |
|:------------:|:---------------:|
| 1            | Y               |
| 2            | B               |
| 3            | A               |
| 4            | X               |
| 5            | L               |
| 6            | R               |
| 7            | ZL              |
| 8            | ZR              |
| 9            | -               |
| 10           | +               |
| 11           | EB Reset        |
| 12           | ATS             |
| 13           | Home            |
| 14           | Screenshot      |
| 15           | *Unused*        |
| 16           | *Unused*        |
| 17           | Square          |

**Note**: The **ZL** button is also reported as pressed when the power/brake handle is in the **Emergency** position.

#### Hat switch

The hat switch data of the HID report represents the input from the **Up**, **Down**, **Left** and **Right** physical buttons. It uses 4 bits (1 nibble) in total. The following data represents the nibble in hexadecimal.

| Button     | Value      |
|:----------:|:----------:|
| Up         | 0x0        |
| Up+Right   | 0x1        |
| Right      | 0x2        |
| Down+Right | 0x3        |
| Down       | 0x4        |
| Down+Left  | 0x5        |
| Left       | 0x6        |
| Up+Left    | 0x7        |
| None       | 0xF        |

#### Axes

The axis data of the HID report represents input from the reverser handle, the power/brake handle, several buttons and the horn pedal. Each axis uses 1 byte.

Axis 1 represents input from the **Horn** button and the horn pedal. Only one of the buttons can be pressed simultaneously.

| Physical Button      | Value |
|:--------------------:|:-----:|
| *No button pressed*  | 0x80  |
| Horn                 | 0xFF  |
| Horn Pedal (Light)   | 0x40  |
| Horn Pedal (Strong)  | 0x00  |

Axis 2 represents the notch of the power/brake handle, where each notch has a specific value. There are no transition values between notches.

| Notch      | Value |
|:----------:|:-----:|
| Emergency  | 0x00  |
| B8         | 0x05  |
| B7         | 0x13  |
| B6         | 0x20  |
| B5         | 0x2E  |
| B4         | 0x3C  |
| B3         | 0x49  |
| B2         | 0x57  |
| B1         | 0x65  |
| N          | 0x80  |
| P1         | 0x9F  |
| P2         | 0xB7  |
| P3         | 0xCE  |
| P4         | 0xE6  |
| P5         | 0xFF  |

Axis 3 represents input from the **Pantograph Down** and **Hill Start** buttons. Only one of the buttons can be pressed simultaneously.

| Physical Button     | Value |
|:-------------------:|:-----:|
| *No button pressed* | 0x80  |
| Pantograph Down     | 0x00  |
| Hill Start          | 0xFF  |

Axis 4 represents the position of the reverser handle, where each position has a specific value. There are no transition values between positions.

| Position   | Value |
|:----------:|:-----:|
| Forward    | 0x80  |
| Neutral    | 0x00  |
| Backward   | 0xFF  |

### Output

The controller has an output HID endpoint to control the door lamp and the **EB Reset** button lamp. The output data follows the structure below.

| Byte #       | Data            |
|:------------:|:---------------:|
| 1            | *Unused*        |
| 2            | *Unused*        |
| 3            | *Unused*        |
| 4            | Door lamp       |
| 5            | EB Reset lamp   |
| 6            | *Unused*        |
| 7            | *Unused*        |
| 8            | *Unused*        |

For each byte, **0x0** turns off the corresponding lamp and any other value turns it on.
