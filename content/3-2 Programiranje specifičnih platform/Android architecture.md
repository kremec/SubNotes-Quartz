Open-source, Linux-based OS optimized for ==battery-powered, low-memory devices== with access to various interfaces
Versions: name and API version (eg. Android 12 supports both API 31 and API 32)
![[Android architecture-Image-1.png|400]]
##### Linux kernel services
==Android automatically manages the process lifecycle== and interprocess communication, file and network I/O, device drivers, ...
Security management: apps run in ==sandboxes==, with ==permissions given by the user==
Power management: screen dimming, process killing, JobScheduler API
##### Native libraries
- System C library
- Surface manager (composing windows), OpenGL (3D graphics)
- OpenMAX, Media Framework (audio / video / image processing)
- SQLite (relational database engine)
- Webkit (browser engine)
##### Android runtime
Compilation process:
- programmer $\rightarrow$ ==Java/Kotlin source==
- ==javac/kotlinc $\rightarrow$ Java bytecode/class files==
- ==Proguard $\rightarrow$ obfuscated Java bytecode/class files==
- ==DX $\rightarrow$ DEX bytecode file==
- ==Zip $\rightarrow$ .apk file (resources + code)==
- ==dex2out $\rightarrow$ .elf file (readable to hardware)==

Process VM - compilation of .apk to native machine code:
- Dalvik (until 4.4 KitKat): ==trace-based just-in-time compilation== (saving storage space, but lower performance)
- Android Runtime - ART (from 5.0 Lollypop): ==ahead-of-time compilation==

Gradle: Automated build system, dependency manager, APK signing, ProGuard support
##### Application framework
- Package manager: manage installed applications
- Window manager: connect view to activity's window
- Content provider: manage inter-application data sharing access
- Location manager / Google Play Location Services: provide location information
- Notification manager: manage sound, vibration, LED flash and content of notifications
- Resource manager: manage (programmatically accessible) application resources
- Activity manager: manage application lifecycle and application stack navigation
- View system: build application UI from a layout definition, slowly deprecated for Jetpack Compose
##### System applications
Handling certain Intents