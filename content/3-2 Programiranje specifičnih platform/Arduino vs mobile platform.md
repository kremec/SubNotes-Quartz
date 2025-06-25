## Arduino platform
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
## Mobile platform
Mobile devices:
- user interaction: touch screen, notifications, other existing services
- context awareness: accelerometer, GPS, camera, microphone, gyroscope, ...
- connectivity: WiFi, Bluetooth, GSM, NFC, ...
### Programming Android
Statically typed language, compilation usually targets JVM (use with / replace Java)
Benefits:
- Coroutines: background processing without spawning threads
- Data class: creates fields, getters/setters, equals, toString, hashCode, ...
- Extension functions: add function to any class without moving it there
- Functions can be stored in variables and passed as arguments
- Null safety: distinct nullable and non-nullable objects, `?` operator, smart cast, ...
- Kotlin Android Extensions (KTX): external library for Android development