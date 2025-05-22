==Platform==: environment in which a software application is executed
- hardware: processing (clock frequency, instruction set, ...) and I/O capabilities (sensors, actuators, ...)
- middleware: drivers, operating system, ...
- higher level: APIs, cloud computing support, ...
### Web platforms
- Highly available (distributed) information storage
- Worldwide connectivity (addressing, routing)
- Stateless (or cookies)

Multi-tier archiecture: flexible scaling and updates
- Presentation layer - frontend (HTML + CSS / AJAX / Angular, React, ... )
- Business layer - backend:
    - web servers (Apache / nginx / ... )
    - frameworks: (Django - Python / ASP.NET - C# / Node.js - JavaScript / ... )
- Data layer:
    - relational databases (PostgreSQL / MySQL / ... )
    - non-relational databases (MongoDB / Cassandra / ... )

MEAN (MongoDB - Express.js - Angular - Node.js): current standard (JavaScript for frontend and backend)
### Mobile platforms
Hardware enables:
- context awareness (sensors - gyroscope, accelerometer, ... )
- wireless connectivity (WiFi, LTE, NFC, ... )

Operating systems:
- Symbian: discontinued (poor UX and DX)
- iOS:
    - Darwin core, runs on specific hardware
    - iOS SDK, Cocoa Touch UI, Swift / Objective-C
- Android:
    - Linux kernel, runs on different hardware platforms
    - Android SDK, Material Design, Kotlin / Java / C++
    - Google services built-in, but OS is opensource $\rightarrow$ possible modifications
### Embedded platforms
98% of computers are embedded
Hardware:
- sensors and actuators: interactions with environment
- wireless communication
- ==memory & energy constraints==

Operating systems:
- None (Arduino bootloader loads your flashed firmware)
- Real-time OS (FreeRTOS - microkernel)
- Specifics (TinyOS - low-power wireless sensor networks)

Programming:
- low-level programming (C / Assembly / ... )
- ==real-time OS== guarantees task handling times
    - low priority tasks execte in infinite loop
    - hight priority event preempts the current task and executes the ==interrupt routine==
### Gaming platforms
High-processing, high-quality graphics