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

| Button 1   | Button 2   | Button 3   | Button 4   | Button 5   | Button 6   | Button 7   | Button 8   | Button 9   | Button 10  | Button 11  | Button 12  | Button 13  | Button 14  | Button 15  | Button 16  | Button 17  |
|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|
| Y          | B          | A          | X          | L          | R          | ZL         | ZR         | -          | +          | EB Reset   | ATS        | Home       | Screenshot | *Unused*   | *Unused*   | Square     |

**Note**: The **ZL** button is also reported as pressed when the power/brake handle is in the **Emergency** position.

#### Hat switch

The hat switch data of the HID report represents the input from the **Up**, **Down**, **Left** and **Right** physical buttons. It uses 4 bits (1 nibble) in total. The following data represents the nibble in hexadecimal.

| Up         | Up+Right   | Right      | Down+Right | Down       | Down+Left  | Left       | Up+Left    | None       |
|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|
| 0x0        | 0x1        | 0x2        | 0x3        | 0x4        | 0x5        | 0x6        | 0x7        | 0xF        |

#### Axes

The axis data of the HID report represents input from the reverser handle, the power/brake handle, several buttons and the horn pedal. Each axis uses 1 byte.

Axis 1 represents input from the **Horn** button and the horn pedal. Only one of the buttons can be pressed simultaneously.

| Released            | Horn                | Horn Pedal (Light)  | Horn Pedal (Strong) |
|:-------------------:|:-------------------:|:-------------------:|:-------------------:|
| 0x80                | 0xFF                | 0x40                | 0x00                |

Axis 2 represents the notch of the power/brake handle, where each notch has a specific value. There are no transition values between notches.

| Emergency | B8   | B7   | B6   | B5   | B4   | B3   | B2   | B1   | N    | P1   | P2   | P3   | P4   | P5   |
|:---------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
| 0x00      | 0x05 | 0x13 | 0x20 | 0x2E | 0x3C | 0x49 | 0x57 | 0x65 | 0x80 | 0x9F | 0xB7 | 0xCE | 0xE6 | 0xFF |

Axis 3 represents input from the **Pantograph Down** and **Hill Start** buttons. Only one of the buttons can be pressed simultaneously.

| Released        | Pantograph Down | Hill Start      |
|:---------------:|:---------------:|:---------------:|
| 0x80            | 0x00            | 0xFF            |

Axis 4 represents the position of the reverser handle, where each position has a specific value. There are no transition values between positions.

| Forward  | Neutral  | Backward |
|:--------:|:--------:|:--------:|
| 0x80     | 0x00     | 0xFF     |

### Output

The controller has an output HID endpoint to control the door lamp and the **EB Reset** button lamp. The output data follows the structure below.

| Byte 1        | Byte 2        | Byte 3        | Byte 4        | Byte 5        | Byte 6        | Byte 7        | Byte 8        |
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
| *Unused*      | *Unused*      | *Unused*      | Door lamp     | EB Reset lamp | *Unused*      | *Unused*      | *Unused*      |

For each byte, **0x0** turns off the corresponding lamp and any other value turns it on.
