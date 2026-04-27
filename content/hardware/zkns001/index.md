---
title: "One handle controller (Nintendo Switch) / ZUIKI Mascon"
hidden: true
---

{{% hardware-overview zkns001 %}}
{{% hardware-support zkns001 %}}

## Technical details

This controller has one handle (5 power notches and 8+emergency brake notches) and 16 buttons.

Internally, it is a HID-compliant joystick with 14 buttons, a hat switch and 4 axes.

|                             |                                                                                                  |
|-----------------------------|--------------------------------------------------------------------------------------------------|
| **Product name**            | One Handle MasCon for Nintendo Switch<br>One Handle MasCon for Nintendo Switch Exclusive Edition |
| **Manufacturer**            | *None*                                                                                           |
| **Vendor/Product ID**       | 0x0F0D/0x00C1 (Densha de GO! edition)<br>0x33DD/0x0002 (Densha de GO! 1st anniversary translucent edition)<br>0x33DD/0x0003 (ZUIKI Mascon Red)<br>0x33DD/0x0004 (ZUIKI Mascon Blue)<br>0x33DD/0x0005 (ZUIKI Mascon Black) |
| **Serial number**           | *None*                                                                                           |
| **USB standard descriptor** | [Download](standard-descriptor.txt)                                                              |
| **HID report descriptor**   | [Download](hid-report-descriptor.txt)                                                            |

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
| 11           | *Unused*        |
| 12           | *Unused*        |
| 13           | Home            |
| 14           | Screenshot      |

{{% notice note %}}
The **ZL** button is also reported as pressed when the power/brake handle is in the **Emergency** position.
{{% /notice %}}

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

The axis data of the HID report represents input from the power/brake handle. Each axis uses 1 byte.

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

Axes 1, 3 and 4 are unused and have a fixed value of **0x80**.
