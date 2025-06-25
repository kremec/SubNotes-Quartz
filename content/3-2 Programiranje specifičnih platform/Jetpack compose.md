Drawback of traditional method:
- writing both XML and Kotlin code
- managing multiple Activities and Fragments
- lots of listeners and other boilerplate to achieve dynamic UI

==Jetpack compose==: modern Android UI toolkit
- declarative - no catches as with Views
- data-driven, reactive - automatic UI updates after underlying state change
- testability and previewing
- type safety

Parts of Jetpack Compose app:
- Activity (usually 1)
- ui.theme - hosts appearance definitions (colors, shapes, theme switching, ...)
- res - storage for drawables, strings, ...
- Gradle scripts

==Composable functions==: Kotlin functions (annotated with `@Composable`) that define UI based on data and user actions, defined outside Activity

State: value that changes over time
Stateful function: remembers the variable over invocations
Recomposition: functions affected by state change are called to recompose UI

State propagates down the hierarchy, events propagate up the hierarchy

Coroutines in composable functions started inside `LaunchedEffect` - composable allowing coroutine launching
#### Navigation
Single Activity
- NavHost component
- NavHostController created and remembered with `rememberNavController()`, call `navigate()` with Destination route as parameter
- Destinations (usually) defined in a separate class
- NavigationBar tied to routes of NavHostController, modifies the content of NavHost component

