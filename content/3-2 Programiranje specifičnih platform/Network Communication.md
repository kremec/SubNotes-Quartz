### Wireless data transmission
Information encoded as variability of electromagnetic fields:
- frequency (f): wave oscillation speed, ==higher f $\rightarrow$ shorter range==
- wavelength ($\lambda$): inverse of frequency, ==higher $\lambda$ $\rightarrow$ longer antenna==
- bandwidth: width of a range of frequencies used, ==more bandwidth $\rightarrow$ higher throughput==

Sender (Tx) includes oscillator DAC, receiver (Rx) includes oscillator ADC
### Smartphone wireless interfaces
Wireless interface selection impact:
- capabilities - transfer speed, coverage area and maximum range
- monetary cost
- power consumption

|                | Near Field Communication (NFC)                          | Bluetooth                                                     | WiFi                                | Cellular network                          |
| -------------- | ------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------- | ----------------------------------------- |
| **Power**      | Low / no                                                | Low (~10mW)                                                   | Medium (~100mW)                     | High (~200mW)                             |
| **Range**      | Short (~10cm)                                           | Short (~10m)                                                  | Medium (~100m)                      | Long (~1km)                               |
| **Throughput** | Low (~400kbps)                                          | Low (~1Mbps)                                                  | High (~100Mbps)                     | Varying (~40kbps with 2G, ~1Gbps with 5G) |
| **Usage**      | Security tags, location-based services, payment systems | Peripherals and wearables, medical equipment, vehicle systems | Large downloads, home entertainment | Real-time updates                         |
Interface management: `NfcManager`, `BluetoothManager`, `WifiManager`, `TelephonyManager`, ...
`ConnectivityManager`: network connections monitoring, connectivity changes notifications
### Networking abstractions
#### Sockets
`Socket` - TCP, `DatagramSocket` - UDP
#### Http(s)URLConnection
HTTP(S) connection and transfers:
- connection pooling $\rightarrow$ socket reuse
- response caching
- cookie management
#### OkHttp (3rd party library)
Advanced HTTP client:
- all features of HttpsURLConnection
- automatic network connection recovery, retries
- data compression
#### Retrofit (3rd party library)
REST client using (OkHttp under the hood):
- define model and REST operations
- define converter and adapter
- define authentication mechanisms

<br><br><br><br>
### Best practices
- Run network operations on a separate thread
- Reduce amount of data transfers:
	- compress data / use low resolution content when possible
	- query only what's needed
	- cache static (and dynamic as much) content
- Get notified on remote data change instead of polling
- Reuse network connections
- Secure connection (SSL) and minimize sensitive data transfers
- Energy-efficient networking:
	- bundle data $\rightarrow$ send data less frequently
	- use WorkManager
- Adapt to available connection:
	- slower network $\rightarrow$ reduce transfers
	- faster network $\rightarrow$ prefetch
### Backend for mobile apps
==Firebase== (Google-developed):
- Authentication with Google ID
- Notifications
- Crashlytics

==Parse server== (open source backend as a service):
- building REST APIs
- cron jobs on server
- user management