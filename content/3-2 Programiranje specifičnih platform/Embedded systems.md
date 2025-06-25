Often for a single application, low price, highly reliable, resource efficiency
### Embedded system pipeline
![[Embedded systems-Image-1.png|400]]
==Intellectual Property Core (IP Core)==: ==Reusable unit of logic/functionality== (eg. network / video / bus protocol / ... chip) $\rightarrow$ ==produced in high volume==
==Field-Programmable Gate Array (FPGA)==: ==Reconfigurable/programmable integrated circuit== for specific functionality $\rightarrow$ ==better performance==
==MicroController Unit (MCU)==: ==Scaled-down microprocessor== sending/receiving commands to connected components $\rightarrow$ ==needs to be programmed==
==Sensors==: Measure physical properties - convert them to electric signals
- Specifications: accuracy, sensitivity, sensing range, sampling interval, type (digital / analogue)

==Actuators==: Cause events to occur in the environment
- Driven by embedded system's signals, often require extra power
### Conversions
#### Analogue-Digital Converter (ADC)
Analogue input (eg. sensor) $\rightarrow$ digital output
Limited number of bits $\rightarrow$ ==quantization error==:
$$
E_{RMS}=\sqrt{\frac1\Delta*\int_{-\frac\Delta2}^{\frac \Delta2}x^2\ dx}=\ ...\ =  \frac\Delta{\sqrt{12}}
$$
$$
\Delta=\frac{range}{2^{bits}}
$$
ADC sampling rate - frequency of conversion and sending data - needs to be high enough
#### Digital-Analogue Converter (DAC)
Digital input (from processor) $\rightarrow$ analogue output (eg. actuator)
==Pulse-Width Modulation==: simulating analogue output
![[Embedded systems-Image-2.png|400]]
<br><br><br><br><br><br><br><br><br><br>
### Designing Embedded System Applications
#### Selecting hardware
Datasheets for complex components
MCU selection based on requirements: word length, clock speed, IO pins, timers, ...
- storage (cost vs speed tradeoff)
- registers (fast, single location)
- register file (a set of registers)
- memory:
    - cache: fast, cheaper than registers (used for data and instruction cache)
    - main memory: connected to CPU via bus $\rightarrow$ slow but large
    - EEPROM: survives power off, but small and slow (used for configuration data)
    - flash: large, faster reads but slower writes than EEPROM, survives power off
#### Programming MCU
MCU (machine language) vs programmer (high level language)
- ==Cross compilation==: programme on PC, deploy to MCU
- ==Toolchain==: development tools
#### Embedded operating systems
Communication, managing tasks/processes and resource allocation
==Process==: abstraction of processing tasks, usually ==1 process per app==
- Separate memory space $\rightarrow$ slower inter-process communication

==Task==: smallest unit of execution, multiple tasks per process - ==fast switching==
- Shared memory space $\rightarrow$ direct inter-task communication (shared variables)
![[Embedded systems-Image-3.png|350]]

==OS is optional==: embedded devices are often single-purpose
- consumes resources (processing, memory, energy)

==OS is useful==:
- easier programming and deployment (provides libraries)
- task-resource allocation support (for complex apps)

==Real-Time Operating System (RTOS)==: event driven OS with a scheduler for time sharing (eg. round-robin / priority preeemptive scheduling / ... )