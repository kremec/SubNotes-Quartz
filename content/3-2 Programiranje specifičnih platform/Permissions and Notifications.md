Applications are ==sandboxed==, have device-unique user ID and group ID
### Permissions
App, through declarations in ==AndroidManifest.xml==, requests access to:
- user data (eg. contacts)
- cost-sensitive APIs (eg. sending SMS)
- system resources (eg. camera)

Permission types:
- normal: OS grants them on installation (eg. `FLASHLIGHT`,  `VIBRATE`, `BLUETOOTH`, ...)
- dangerous: OS asks user to grant access when functionality is about to be used (eg. `READ_CONTACTS`, `SEND_SMS`, ...)
- special: toggles in Special app access page in system (eg. `MANAGE_EXTERNAL_STORAGE`)
- custom: permission for other apps to launch your app's components (Activities, Services, BroadcastReceivers, ContentProviders)

Good practices:
- request only needed permissions, use other apps through Intents if possible
- show immediate benefits of granting permissions to users
### Notifications
Shown in the Status (Notification) Bar
Support: custom icons, sound and visual alerts; shown in notification drawer, on lockscreen

Implementation of notification:
- management: ==NotificationManagerCompat== - `notify()`, `cancel()`, `cancelAll()`
- building: ==NotificationCompat.Builder== - `setContentTitle()`, `setContentText()`, `setSmallIcon()`, `setContentIntent()`

==Notification channels== (from API26): settings management for similarly-themed notifications

Good practices:
- do not overuse, minimise interruptions