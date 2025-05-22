Open-source designs $\rightarrow$ large developer community
#### Arduino Uno board
==MCU==: 8bit ATmega328, 20MHz (programming) and ATmega16U2 (USB communication)
==USB interface==: programming and power
==IO pins==: wired to MCU, power / digital IO (read `LOW`/`HIGH` or write 0V/5V)
==Reset button==: restarts app (but app and bootloader remain loaded)
#### Arduino shields
Add functionalities (eg. Ethernet, LCD, GPS, ... )
#### Arduino software
Arduino bootloader: runs first for environment setup
==Sketches==: Arduino programmes written in C in `.ino` files
- `setup()`: fired once on power on - inicialization
- `loop()`: infinite loop starts after `setup()`
### Arduino programming
`pinMode` ... `INPUT` / `OUTPUT` / `INPUT_PULLUP`
`analogWrite` is emulated with a PWM wave (affecting the average voltage)

Interrupt: signal telling MCU about an event requiring immediate attention, interrupt handlers are not pre-emptive

Global variables: reduced memory overhead, simplicity