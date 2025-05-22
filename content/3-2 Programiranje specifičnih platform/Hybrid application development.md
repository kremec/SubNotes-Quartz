Idea: ==write programme once, run on all different platforms/vendors== (eg. desktop, Android, iOS, ...)
### Web views (Apache Cordova)
Drawbacks:
- only lowest common denominator subset of internal platform functionalities available
- translation can lead to inefficiencies
- different platforms have different user interface conventions
### Web apps (React Native)
Use common language, libraries implement access to specific internal platform functionalities
### Build own language and rendering engine (Flutter)
Plugins/platform channels implement access to internal platform functionalities
Custom language: Dart
Everything is a Widget (Stateless and Stateful widgets) $\rightarrow$ Widget trees