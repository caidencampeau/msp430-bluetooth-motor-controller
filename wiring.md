# Wiring Reference

The connections below are taken from the project's final report. This is a **pin map**, not a verified production schematic.

## HM-10 Bluetooth → MSP430FR2355

| HM-10 | MSP430 | Purpose |
| --- | --- | --- |
| TXD | P1.6 (UART RX) | Bluetooth commands to MSP430 |
| RXD | P1.7 (UART TX) | Status messages to phone |
| GND | Common ground | Signal ground |
| VCC | *Not specified in report* | Power; confirm requirements for your module revision |

UART is configured at **9600 baud** in the project firmware.

## I²C LCD → MSP430FR2355

| LCD / I²C backpack | MSP430 | Purpose |
| --- | --- | --- |
| SDA | P4.6 | I²C data |
| SCL | P4.7 | I²C clock |
| VCC | 3.3 V | LCD supply in the reported build |
| GND | Common ground | Ground |

The firmware uses I²C address **`0x27`**. Confirm that the specific LCD backpack supports the reported supply and logic levels.

## L298N motor driver → MSP430FR2355

| L298N | Connection | Purpose |
| --- | --- | --- |
| ENA | P6.1 (Timer_B PWM) | Duty-cycle control |
| IN1 | P3.0 | Fixed forward direction |
| IN2 | P3.1 | Fixed forward direction |
| OUT1 / OUT2 | DC motor terminals | Drive motor |
| GND | Common ground | Motor/control shared ground |
| `+12V` supply terminal | +9 V battery terminal (original build) | Motor driver input supply |

Direction is set in firmware as **IN1 high, IN2 low**. The project does not implement reverse-direction commands.

## Power notes

- The **MSP430 LaunchPad was USB powered** in the documented build.
- The **motor/driver were powered by a separate 9 V battery** connected to the L298N supply input.
- The **battery ground and MSP430 ground were connected together**.
- The report does not identify the HM-10 VCC source or fully document all level-shifting/pull-up details. Check those requirements before duplicating the wiring.
- A small rectangular 9 V battery is not generally a robust power source for a DC motor under load; use an appropriately rated supply for extended testing, with a common ground and correct voltage ratings.

For the conceptual diagram, see [`images/system-overview.png`](images/system-overview.png).
