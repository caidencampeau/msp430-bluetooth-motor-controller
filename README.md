# MSP430 Bluetooth DC Motor Controller

**Wireless PWM motor control with an MSP430FR2355, HM-10 Bluetooth module, L298N motor driver, and 16×2 I²C LCD.**

A phone sends speed commands over Bluetooth Low Energy (BLE) to the HM-10. The MSP430 reads those commands over UART, updates the motor's PWM duty cycle, displays the selected percentage on the LCD, and sends a confirmation back to the phone.

![Conceptual hardware overview showing the motor, L298N, MSP430 LaunchPad, LCD, Bluetooth module and phone](docs/images/system-overview.png)

### Demo

[Watch the working project on YouTube](https://youtube.com/shorts/Rp66Ol3cZnw?feature=share)

### What it demonstrates

- **Embedded control:** MSP430FR2355 and Timer_B PWM output to the L298N motor driver.
- **Wireless communication:** HM-10 BLE module interfaced using **9600-baud UART**.
- **Peripheral integration:** 16×2 LCD through **I²C** (address `0x27`).
- **Interrupt-driven input:** UART receive interrupt processes new commands; the main loop updates the output and display.
- **User feedback:** Requested speed percentage shown on the LCD and echoed to the Bluetooth terminal.

### Hardware

| Component | Role |
| --- | --- |
| TI MSP-EXP430FR2355 LaunchPad | Main controller |
| HM-10 BLE UART module | Phone-to-MSP430 command interface |
| L298N H-bridge module | Motor drive and PWM enable |
| DC motor (described as 12 V in report) | Controlled load |
| 16×2 LCD with I²C backpack | Displays duty-cycle percentage |
| 9 V battery + USB | Original demonstration power arrangement |

### Commands

Send **one character** using the DSD Tech Bluetooth terminal app:

| Input | PWM duty-cycle command |
| --- | --- |
| `0`–`9` | 0%, 10%, …, 90% respectively |
| `A` or `a` | 100% |
| `B` or `b` | Stop (0%) |

After each valid command, the LCD updates and the MSP430 responds with text such as `speed = 50%`.

### Project status

**Completed class demonstration (July 2026).**
