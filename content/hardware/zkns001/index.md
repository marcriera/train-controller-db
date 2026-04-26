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

| Button 1   | Button 2   | Button 3   | Button 4   | Button 5   | Button 6   | Button 7   | Button 8   | Button 9   | Button 10  | Button 11  | Button 12  | Button 13  | Button 14  |
|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|
| Y          | B          | A          | X          | L          | R          | ZL         | ZR         | -          | +          | *Unused*   | *Unused*   | Home       | Screenshot |

**Note**: The **ZL** button is also reported as pressed when the power/brake handle is in the **Emergency** position.

#### Hat switch

The hat switch data of the HID report represents the input from the **Up**, **Down**, **Left** and **Right** physical buttons. It uses 4 bits (1 nibble) in total. The following data represents the nibble in hexadecimal.

| Up         | Up+Right   | Right      | Down+Right | Down       | Down+Left  | Left       | Up+Left    | None       |
|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|
| 0x0        | 0x1        | 0x2        | 0x3        | 0x4        | 0x5        | 0x6        | 0x7        | 0xF        |

#### Axes

The axis data of the HID report represents input from the power/brake handle. Each axis uses 1 byte.

Axis 2 represents the notch of the power/brake handle, where each notch has a specific value. There are no transition values between notches.

| Emergency | B8   | B7   | B6   | B5   | B4   | B3   | B2   | B1   | N    | P1   | P2   | P3   | P4   | P5   |
|:---------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
| 0x00      | 0x05 | 0x13 | 0x20 | 0x2E | 0x3C | 0x49 | 0x57 | 0x65 | 0x80 | 0x9F | 0xB7 | 0xCE | 0xE6 | 0xFF |

Axes 1, 3 and 4 are unused and have a fixed value of **0x80**.
