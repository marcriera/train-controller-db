---
title: 'Two handle controller "Type 2" (Sony PlayStation 2)'
hidden: true
---

{{% hardware-overview tcpp20009 %}}
{{% hardware-support tcpp20009 %}}

## Technical details

This controller has 2 handles (5 power notches and 8+emergency brake notches), a D-Pad and 6 buttons (Select, Start, A, B, C, D). In addition, it provides a door lamp and a 3.5 mm jack connector to plug a horn pedal. There are 2 rumble motors, one in each handle.

Internally, it is a vendor-specific class device. The input data is compatible with HID, but the device does not provide a HID descriptor.

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | TAITO_DENSYA_CON_T01                      |
| **Manufacturer**            | TAITO                                     |
| **Vendor ID**               | 0x0AE4                                    |
| **Product ID**              | 0x0004                                    |
| **Serial number**           | TCPP20010                                 |
| **USB standard descriptor** | [Download](standard-descriptor.txt) |
| **HID report descriptor**   | [Download](hid-report-descriptor.txt) (recreated, not provided by actual device) |

### Input

The controller sends reports to the host (PS2) formed by 6 bytes:

| Byte # | Data            |
|:------:|:---------------:|
| 1      | 0x01 (*fixed*)  |
| 2      | Brake           |
| 3      | Power           |
| 4      | Pedal           |
| 5      | D-Pad           |
| 6      | Buttons         |

The values for the brake notch byte are the following. Between notches, a transition value of **0xFF** is reported.

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

The values for the power notch byte are the following. Between notches, a transition value of **0xFF** is reported.

| Notch      | Value |
|:----------:|:-----:|
| N          | 0x81  |
| P1         | 0x6D  |
| P2         | 0x54  |
| P3         | 0x3F  |
| P4         | 0x21  |
| P5         | 0x00  |

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
| 1   | B               |
| 2   | A               |
| 3   | C               |
| 4   | D               |
| 5   | Select          |
| 6   | Start           |
| 7   | *Unused*        |
| 8   | *Unused*        |

### Output

The controller supports receiving data via a control transfer to turn on/off the door lamp and provide rumble. The setup packet is as follows:

| Data          | Value       |
|:-------------:|:-----------:|
| bmRequestType | 0x41        |
| bRequest      | 0x09        |
| wValue        | 0x0201      |
| wIndex        | 0x0         |
| wLength       | 0x2         |

The data sent to the controller follows the structure below.

| Byte # | Value    |
|:------:|:--------:|
| 1      | Status   |
| 2      | Function |

* **Status:** defines whether the function specified in byte 2 is **Off** (**0x00**) or **On** (**0x01**).
* **Function:** **0x01** is **Left rumble**, **0x02** is **Right rumble**, **0x03** is **Door lamp**.
