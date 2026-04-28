---
title: "Master Controller (PC)"
hidden: true
---

{{% hardware-overview vok00105 %}}
{{% hardware-support vok00105 %}}

## Technical details

This controller has one handle (with adjustable notches), a reverser switch with 3 positions (F, N, B) and 4 buttons (S, A, B, C). It was manufactured by Pony Canyon. It requires external power to work, either with an included power supply or 4 AA-sized batteries.

It connects to PC via serial cable, either directly via a DE-9 connector or with a USB adapter.

|                  |       |
|------------------|-------|
| **Baud rate**    | 19200 |
| **Data bits**    | 8     |
| **Parity**       | None  |
| **Stop bits**    | 1     |
| **Flow control** | None  |

Unlike other controllers, the notches in the combined power-brake handle are adjustable. On the underside of the controller there are a sliding switch, as well as a window with dip switches, to change gears. This change can be done with the controller turned off. The notch print beside the handle can also be changed to match the current gear setting.

The are 8 possible gear settings:

| Setting   | Power notches | Brake notches |
|:---------:|:-------------:|:-------------:|
| Type A    | 4             | 5             |
| Type B    | 3             | 7             |
| Type C    | 5             | 5             |
| Type D    | 4             | 7             |
| Type E    | 4             | 8             |
| Type F    | 5             | 8             |
| Type G    | 5             | 7             |
| Type H    | 6 (no click)  | 8 (no click)  |

### Input

The controller sends 5-character events separated by a carriage return (ASCII *0xD*).

Events for the handle are the following.

| Notch     | Event |
|:---------:|:-----:|
| Emergency | TSB20 |
| B8        | TSB30 |
| B7        | TSB40 |
| B6        | TSE99 |
| B5        | TSA05 |
| B4        | TSA15 |
| B3        | TSA25 |
| B2        | TSA35 |
| B1        | TSA45 |
| N         | TSA50 |
| P1        | TSA55 |
| P2        | TSA65 |
| P3        | TSA75 |
| P4        | TSA85 |
| P5        | TSA95 |
| P6        | TSB60 |

Events for the reverser are the following.

| Position | Event |
|:--------:|:-----:|
| Forward  | TSG99 |
| Neutral  | TSG50 |
| Backward | TSG00 |

Events for the buttons are the following. One event is reported when the button is pressed, and another event when the button is released.

| Button | Press Event | Release Event |
|:------:|:-----------:|:-------------:|
| S      | TSK99       | TSK00         |
| A      | TSX99       | TSX00         |
| B      | TSY99       | TSY00         |
| C      | TSZ99       | TSZ00         |
