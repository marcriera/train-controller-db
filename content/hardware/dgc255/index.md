---
title: "One handle controller (PC)"
hidden: true
---

{{% hardware-overview dgc255 %}}
{{% hardware-support dgc255 %}}

## Technical details

This controller has one handle (5 power notches and 8+emergency brake notches), a D-Pad and 6 buttons (Select, Start, A, B, C, D).

Internally, it is a HID-compliant joystick with two axes, 6 buttons and a hat switch.

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | *Unknown*                                 |
| **Manufacturer**            | *Unknown*                                 |
| **Vendor ID**               | 0x0AE4                                    |
| **Product ID**              | 0x0003                                    |
| **Serial number**           | *Unknown*                                 |
| **USB standard descriptor** | *Not available*                           |
| **HID report descriptor**   | *Not available*                           |

The controller uses the same IDs as the [DGOC-44U controller]({{% relref dgoc44u %}}) and sends compatible HID reports. The games check if the controller has a hat switch to distinguish between models.

### Input

#### Buttons

The button data of the HID report represents input from most physical buttons. Each button in the HID report uses one bit. **0** means that the button is released and **1** that it is pressed.

| HID Button # | Physical Button |
|:------------:|:---------------:|
| 1            | B               |
| 2            | A               |
| 3            | C               |
| 4            | D               |
| 5            | Select          |
| 6            | Start           |

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

Axis 1 represents the brake notch, where each notch has a specific value. If the brake/power handle is in a power notch, **N** is reported. Between notches, a transition value of **0xFF** is reported.

| Notch      | Value |
|:----------:|:-----:|
| Emergency  | 0xB9  |
| B8         | 0xB5  |
| B7         | 0xB2  |
| B6         | 0xAF  |
| B5         | 0xA8  |
| B4         | 0xA2  |
| B3         | 0x9A  |
| B2         | 0x94  |
| B1         | 0x8A  |
| N          | 0x79  |

Axis 2 represents the power notch, where each notch has a specific value. If the brake/power handle is in a brake notch, **N** is reported. Between notches, a transition value of **0xFF** is reported.

| Notch      | Value |
|:----------:|:-----:|
| N          | 0x81  |
| P1         | 0x6D  |
| P2         | 0x54  |
| P3         | 0x3F  |
| P4         | 0x21  |
| P5         | 0x00  |
