---
title: "Two handle controller (PC)"
hidden: true
---

{{% hardware-overview dgoc44u %}}
{{% hardware-support dgoc44u %}}

## Technical details

This controller has two handles (5 power notches and 8+emergency brake notches) and 6 buttons (Select, Start, A, B, C, D).

Internally, it is a HID-compliant joystick with 2 axes and 6 buttons.

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | 電車でGO! コントローラ USB版                  |
| **Manufacturer**            | TAITO                                     |
| **Vendor ID**               | 0x0AE4                                    |
| **Product ID**              | 0x0003                                    |
| **Serial number**           | TCPP20009                                 |
| **USB standard descriptor** | [Download](standard-descriptor.txt) |
| **HID report descriptor**   | [Download](hid-report-descriptor.txt) |

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

#### Axes

The axis data of the HID report represents input from the power and brake handles. Each axis uses 1 byte.

Axis 1 represents the notch of the brake handle, where each notch has a specific value. Between notches, a transition value of **0xFF** is reported.

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
| Released   | 0x79  |

{{% notice note %}}
There are 5 unmarked positions between **B8** and **Emergency**, which all report the value for **Emergency**.
{{% /notice %}}

Axis 2 represents the notch of the power handle, where each notch has a specific value. Between notches, a transition value of **0xFF** is reported.

| Notch      | Value |
|:----------:|:-----:|
| N          | 0x81  |
| P1         | 0x6D  |
| P2         | 0x54  |
| P3         | 0x3F  |
| P4         | 0x21  |
| P5         | 0x00  |
