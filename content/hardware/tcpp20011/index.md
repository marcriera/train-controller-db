---
title: "Shinkansen controller (Sony PlayStation 2)"
hidden: true
---

{{% hardware-overview tcpp20011 %}}
{{% hardware-support tcpp20011 %}}

## Technical details

This controller has 2 handles (13 power notches and 7+emergency brake notches), a D-Pad and 6 buttons (Select, Start, A, B, C, D). In addition, it provides a simple display, a door lamp and a 3.5 mm jack connector to plug a horn pedal. There are 2 rumble motors, one in each handle.

Internally, it is a vendor-specific class device. The input data is compatible with HID, but the device does not provide a HID descriptor.

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | TAITO_DENSYA_CON_T02                      |
| **Manufacturer**            | TAITO                                     |
| **Vendor ID**               | 0x0AE4                                    |
| **Product ID**              | 0x0005                                    |
| **Serial number**           | TCPP20011                                 |
| **USB standard descriptor** | [Download](standard-descriptor.txt) |
| **HID report descriptor**   | [Download](hid-report-descriptor.txt) (recreated, not provided by actual device) |

### Input

The controller sends reports to the host (PS2) formed by 6 bytes:

| Byte # | Data            |
|:------:|:---------------:|
| 1      | Brake           |
| 2      | Power           |
| 3      | Pedal           |
| 4      | D-Pad           |
| 5      | Buttons         |
| 6      | *Unused*        |

The values for the brake notch byte are the following. Between notches, a transition value of **0xFF** is reported.

| Notch      | Value |
|:----------:|:-----:|
| Emergency  | 0xFB  |
| B7         | 0xDF  |
| B6         | 0xC3  |
| B5         | 0xA7  |
| B4         | 0x8B  |
| B3         | 0x70  |
| B2         | 0x54  |
| B1         | 0x38  |
| Released   | 0x1C  |

The values for the power notch byte are the following. Between notches, a transition value of **0xFF** is reported.

| Notch      | Value |
|:----------:|:-----:|
| N          | 0x12  |
| P1         | 0x24  |
| P2         | 0x36  |
| P3         | 0x48  |
| P4         | 0x5A  |
| P5         | 0x6C  |
| P6         | 0x7E  |
| P7         | 0x90  |
| P8         | 0xA2  |
| P9         | 0xB4  |
| P10        | 0xC6  |
| P11        | 0xD7  |
| P12        | 0xE9  |
| P13        | 0xFB  |

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
| 1   | D               |
| 2   | C               |
| 3   | B               |
| 4   | A               |
| 5   | Select          |
| 6   | Start           |
| 7   | *Unused*        |
| 8   | *Unused*        |

### Output

The controller supports receiving data via a control transfer to update the screen, turn on/off the door lamp and provide rumble. The setup packet is as follows:

| Data          | Value       |
|:-------------:|:-----------:|
| bmRequestType | 0x40        |
| bRequest      | 0x09        |
| wValue        | 0x0301      |
| wIndex        | 0x0         |
| wLength       | 0x8         |

The data sent to the controller follows the structure below.

| Byte #              | Value                      |
|:-------------------:|:--------------------------:|
| 1                   | Left rumble                |
| 2                   | Right rumble               |
| 3                   | Door lamp + Limit approach |
| 4                   | Speed gauge                |
| 5+6 (Little Endian) | Speedometer                |
| 7+8 (Little Endian) | ATC limit                  |

* **Left/right rumble:** **0x00** is **Off**, **0x01** is **On**.
* **Door lamp:** **0x0X** is **Off**, **0x8X** is **On**.
* **Limit approach:** values between **0xX0** and **0xXA** representing the number of LEDs lit above the speedometer. In-game, these mark the 10 km/h right below the speed limit.
* **Speed gauge:** values between **0x00** and **0x16** representing the number of LEDs lit on the speed gauge. LED #23 cannot be lit. In-game, these mark 15 km/h increments in the current speed, with one lit when speed is 1-15 km/h, two when 16-30 km/h, etc.
* **Speedometer:** values between **0x0000** and **0x0999** representing the current speed. Values are encoded with **BCD 8421** (i.e. **120 km/h** should be represented as **0x0120**, NOT **0x0078**).
* **ATC limit:** values between **0x0000** and **0x0999** representing the ATC speed limit. Values are encoded with **BCD 8421** (i.e. **120 km/h** should be represented as **0x0120**, NOT **0x0078**).
