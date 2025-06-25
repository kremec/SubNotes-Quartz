### Threads
Most general method
==UI (main) thread==:
- infinite loop of UI event listening
- custom code by default $\rightarrow$ run processing-heavy operations on ==background threads== to not impact UI responsiveness
### Services
By default ran on main thread (without UI), for long-running operations on other threads
Create services:
- `Context.startService()` - only 1 service at once (but `onStartCommand()` called each time)
- implicity with `Context.bindService()`

Stop services:
- `stopSelf()` within service
- `Context.stopService()` from another component

==Background service==: actions not noticable by user (eg. periodic updates)
==Foreground service==: actions user sees/controls (eg. music player app) - shows ==sticky notifications==
- Minimizing background processing + immediate guaranteed tasks
    - declare service type (eg. `mediaPlayback`, `camera|microphone`)
    - declare permissions (`FOREGROUND_SERVICE`, `POST_NOTIFICATIONS` needed, eg `FOREGROUND_SERVICE_CAMERA` for specific services)

==Bound services==: remain running as long as connection from client is established
#### Broadcast
==Broadcast==: message sent from other component of your app / other apps / Android system
- Messages ==wrapped in Intents== before sent: `sendBroadcast()` / system-generated broadcasts

Captured in `onReceive()` if BroadcastReceiver is
- dynamically registered for specific broadcast Intents
- statically registered in app manifest $\rightarrow$ OS will wake up app and capture event

Service-Activity communication:
- Activity: implements BroadcastReceiver with `onReceive()`, register to Service results
- Service: `sendBroadcast()` using same Intent action
### Kotlin Coroutines
No Thread (they launched from) blocking - "light" reuse of Threads
`suspend` functions can be paused / resumed

==Coroutine scopes==:
- Lifecycle scope: tied to component's lifecycle
- ViewModel scope: tied to ViewModel's lifecycle
- GlobalScope: tied with app's lifecycle

==Dispatchers== designate Threads for Coroutines to run:
- `Dispatchers.Main` (UI cannot be accessed from background Threads)
- `Dispatchers.IO` and `Dispatchers.Default` - background task Threads (eg. downloads, ...)

Launching Coroutines:
- `launch()` $\rightarrow$ doesn't return result to caller
- `async` $\rightarrow$ allows caller to wait for result with `await()`
- `withContext` - switch to a different context (eg. from Main context launch Coroutine in Default context to change UI)
<br><br><br><br><br><br>
### Periodic / Occasional Task Scheduling
Long/frequent processing $\rightarrow$ inefficient usage of limited battery capacity $\rightarrow$ limit background processing
#### Wake Lock
App prevents phone from going to low-powered sleep mode
Special permission: `WAKE_LOCK`, use `FLAG_KEEP_SCREED_ON` to prevent screen from darkening
#### AlarmManager
Running periodic operations on specific times / time intervals
Alarm types - exactness:
- ==Inexact==: Android manages grouping for battery optimisation
- ==Exact==: executed at prescribed time, unless device is sleeping
- ==Exact while idle==: executed at prescribed time, even if device is sleeping
- ==setAlarmClock==: actual clock alarms, permission `USE_EXACT_ALARM`
  Alarm types - clock:
    - `RTC_WAKEUP`: real-time clock
    - `ELAPSED_TIME`: time since booted

Usage:
- create BroadcastReceiver to execute on alarm
- set alarm: type, starting time, (optional) repeating interval, Intent

Restoring alarms when cancelled if device is rebooted:
- acquire `RECEIVE_BOOT_COMPLETED` permission
- register and create receiver, set alarm in `onReceive()` - when booted back

Do not use for:
- periodic backups $\rightarrow$ WorkManager
- checking for notifications/messages from server $\rightarrow$ Firebase messaging
### Doze mode
Device not charging nor actively used $\rightarrow$ doze mode:
- periodic maintenence periods to perform backlog tasks
- sleep time - wake locks ignored, network access suspended, AlarmManager deferred, ...

Request to be exempt from doze with `REQUEST_IGNORE_BATTERY_OPTIMIZATIONS` permission
### WorkManager
==Guaranteed deferrable constraint-aware execution==
==Worker==: unit of work in `doWork()` by defualt runs on background Thread
==WorkRequest==: set constraints and types of execution of work (eg. device must be charging / idle / ...)
WorkManager CoroutineWorker: work is done in Coroutine $\rightarrow$ more efficient
### When to use what
==Best effort execution - Coroutines== (eg. update UI which may temporarily unavailable in background)
==Guaranteed execution at current moment - ForegroundService, WorkManager== (eg. when user hits pay button the transaction is processed)
==Guaranteed eventual execution - WorkManager== (eg. reminding user to exercise)
==Guaraneteed execution at exact (periodic) times== - extremely difficult:
- make app exempt from battery optimization
- use foreground service
- use AlarmManager exact alarms
- use Firebase Cloud Messeging

==Synchronise data with server - Sync Adapter, WorkManager==
==Download large content in background - Download Manager==
==Location-based execution - Geofencing with Google Play Services==