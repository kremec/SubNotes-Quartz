### Embedded systems & Arduino
```arduino
int pinLed = 2;
int pinButton = 4;
int pinControl = A0;
int data[50];

void liteUp() {
	digitalWrite(pinLed, HIGH);
}

void setup() {
	pinMode(pinLed, OUTPUT);
	pinMode(pinButton, INPUT);

	attachInterrupt(digitalPinToInterrupt(pinButton), liteUp, FALLING);
}

void loop() {
	int delayTime = analogRead(pinControl);
	delay(delayTime);

	analogWrite(pinFan, 255);
}
```
No preemptive interrupts: interrupt on a pin for which ISR is active $\rightarrow$ wait for ISR to finish before being serviced

Volatile: compiler does not see `liteUp` being called $\rightarrow$ it thinks it is always false and is never reread

Input pins:
- Digital pins: read `HIGH`/`LOW` value as input
- Analog pins: ADC converts voltage to a number between 0 and 1023

Ouput pins:
- Digital pins: output `HIGH`/`LOW` electrical signal as output
- Analog pins: PMW wave simulates analog output with values between 0 and 255
### Web platform
TCP: slow connection-based protocol providing reliability and congestion control (slow start) $\rightarrow$ on slow links:
- ACK will not arrive in time $\rightarrow$ receiver will consider packets lost
- congestion control takes a while before fully opening transmittion window

UDP: fast lightweight data stream with no reliability

HTTP: resource heavy request-response communication with connection maintenance and overhead (headers, cookies, ...)

IaaS - Infrastructure as a Service: access to cloud hardware for customer apps to auto-scale (AWS)
PaaS - Platform as a Service: access to whole cloud platform for customer apps to auto-scale (Google App Engine)
SaaS - Software as a Service: whole app lives in the cloud (MS Office 265)

Content addressable / information centric network: nearer content will be used as cache

REST: stateless client-server communication architechture with cacheability
### Android
Android activity lifecycle: resource management, prioritization of multitasking with state preservation
![[Activity, Lifecycle, Intents-Image-1.png|350]]

MVC: Model (SQLite) manages data, Controller (Activity/Fragment) responds to user input, View (XML layout) displays data to user
- Controller and View are tightly connected (changes on one require changes on the other)
- Controller heavily depends on user interaction (and bound lifecycle)

MVVM: ViewModel wraps Model and prepares observable data for Views to use
- VM data can be observed by many Views without VM knowing the observers
- VM survives Activity/Fragment lifecycle changes

LiveData: observable data notifies observers when data changes, lifecycle-aware updates of observers
### Kotlin
```kotlin
private val processingScope = CoroutineScope(Dispatchers.DEFAULT)
private suspend fun downloadPhoto(imageUrl: String) {
	val bitmap = ...
	withContext(Dispatchers.MAIN) {
		imageView.setImageResource(bitmap)
	}
}

class MainActivity(): AppCompatActivity() {
	companion object {
		val TAG = "MainActivity"
	}

	override fun OnCreate(savedInstaceState: Bundle) {
		super.onCreate(savedInstanceState)
		setContentView(R.layout.activity_main)
	}
}
```
### Android app design
MainActivity: ComponentActivity  -  NavHost + NavController
$\downarrow$
Composable screen  -  LazyList, ...
$\updownarrow$  StateFlow
ViewModel
$\updownarrow$  MutableStateFlow
Repository  -  operations on IO threads - Coroutines
$\updownarrow$  DTOs
RestApi (`@Get`) $\leftrightarrow$ Retrofit, GSON (de)serializer
DAO (`@Query`), models (`@Entity`) $\leftrightarrow$ RoomDB
SharedPreferences