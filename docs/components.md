---
id: components
title: Component Kit
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Check out all of these components that can do so many things!

---

### 7-color Flash LED

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="7-color Flash LED"
src={useBaseUrl('img/components/7-color_flash_led.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Analog Hall Effect Sensor

HW-495

<img
alt="Analog Hall Effect Sensor"
src={useBaseUrl('img/components/analog_hall_effect_sensor.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Analog Temperature Sensor

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Analog Temperature Sensor"
src={useBaseUrl('img/components/analog_temperature_sensor.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
#include <math.h> //needed to calculate th

double ConvertTemp(int RawTemp) { //convert raw sensor data to a useable temperature, lots of math

  double Temp;
  Temp = log(10000.0*((1024.0/RawTemp-1)));
  Temp = 1 / (0.001129148 + (0.000234125 + (0.0000000876741 * Temp * Temp ))* Temp );
  Temp=Temp-273.15;
  Temp = (Temp * 9.0)/ 5.0 + 32.0; // Convert Celcius to Fahrenheit
  return Temp;
}

int sensorPin = A2; // select the input pin for the potentiometer, can change this to any pin
                    // with a triangle next to it on the dragontail

void setup() {
  Serial.begin(9600); //serial monitor, available on ArduinoIDE
}

void loop() {
  int readVal=analogRead(sensorPin); //read sensor data
  double temp =  ConvertTemp(readVal); //convert temperature data

 Serial.println(temp);  // display tempature on the serial monitor
 delay(500);
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Avoidance Sensor

_by Leon X. Durrenberger, M.D., Ph. D., Professor Emeritus, Grand Challenge Scholar, and avid conservative thinker._

If you want to use the infrared emitter and receiver to detect a specific distance, then this is the module for you!
The obstacle avoidance sensor will emit a LOW signal if an object is detected, and a HIGH signal otherwise.
It's very useful if you want to make sure that something stays a specific distance away from your project!

To find this sensor, find one with the word "KeyesIR" in the middle.

<img
alt="Avoidance Sensor"
src={useBaseUrl('img/components/avoidance_sensor.jpg')}
class="component-image"
/>

There's a few weird things about this sensor that's customizable:

- The left potentiometer controls the distance that it detects as the threshold
- The right potentiometer controls the frequency of the emitter. **You must turn this one clockwise all the way for it to work**.
- There is a jumper above the right potentiometer that connects two pins labeled `EN`.
  If for any reason you want to only enable your sensor at certain points, take off this jumper, and send a HIGH signal to the `EN` pin
  when you want it to run. Only do this if you are using way too much power.

(For the context of these instructions, hold the sensor so that the emitter and receiver are facing up/on top.)

Other things to know about this sensor:

- There is an LED that lights up, labeled `Sled`, that will light up whenever the pin `out` emits a `LOW` signal (aka whenever an
  object is detected). I have a vague idea that sled means signal LED, but come up with a fun name for it for yourself! I have named
  mine Samuel.
- I've found that this module works most consistently when both potentiometers are turned completely clockwise.
- The max range of the turning for each of the potentiometers is around 90 degrees, and they are relatively hard to turn. I wasn't
  able to turn them with my fingers alone, but I might just be a weakling.
- The potentiometers are the things on top of the blue parts near the bottom of the sensor.

For the example code, plug `GND` to `-`, `+` to `+`, and `out` to pin 16.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
int ledPin = LED_BUILTIN;      // LED pin on arduino
int detectorPin = 16;  // obstacle avoidance sensor interface
int val;              // variable to store result
//int enablePin = 2;  // sensor enable interface (EN)

void setup()
{
  pinMode(ledPin, OUTPUT);  // Define LED as output interface
  pinMode(detectorPin, INPUT);  // Define obstacle avoidance sensor as input interface

  // [uncomment and remove jumper on module to use enable pin (EN)]
  //pinMode(enablePin, OUTPUT);
  //digitalWrite(enablePin, HIGH);  // Enable sensor
}

void loop()
{
  val = digitalRead(detectorPin); // Read value from sensor
  if(val == LOW) // When the sensor detects an obstacle, the LED on the Arduino lights up
  {
    digitalWrite(ledPin, HIGH);
  }
  else
  {
    digitalWrite(ledPin, LOW);
  }
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Ball Switch

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Ball Switch"
src={useBaseUrl('img/components/ball_switch.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Button

Part: HW-483

<img
alt="Button"
src={useBaseUrl('img/components/buttonAlone.jpg')}
class="component-image"
/>

The pushbutton is pretty straightforward: you can use it as an input, and check whether is pushing the button or not. As you can see in the diagram above, left == gnd, center == vdd, and right == data.
Note: A low input indicates that the button is pressed.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
const int buttonPin = 2; //set these as constants
int buttonState = 0;

void setup() {
  pinMode(LED_BUILTIN, OUTPUT); //using the inbuilt LED on the back of the clue!
  pinMode(buttonPin, INPUT); //set the pushbutton sensor as an input
}

void loop() {
  buttonState = digitalRead(buttonPin);//read the state of the button

  if (buttonState == HIGH) { //if the button is NOT pressed
    //turn LED on
    digitalWrite(LED_BUILTIN, HIGH);
  } else { //if the button is pressed
    // turn LED off:
    digitalWrite(LED_BUILTIN, LOW);
  }
}
```

</TabItem>
<TabItem value="py">

```py
import board
import digitalio
import time
#here I decide to use an LED to check the status of the button
led = digitalio.DigitalInOut(board.D7) #set led pin
button = digitalio.DigitalInOut(board.D1) #set button pin
led.direction = digitalio.Direction.OUTPUT
button.direction = digitalio.Direction.INPUT

while True:
  if button.value: #if the button is off
    led.value = False #led is off
  else: #if the button is on
    led.value = True #led is on
```

</TabItem>
</Tabs>

---

### Buzzer

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Buzzer"
src={useBaseUrl('img/components/buzzer.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Digital Temperature Sensor

This sensor monitors temperature and, if the temperature is above a specific threshold, outputs a logical 1. If the temp is below the threshold, it outputs a 0. How do you set this threshold? Why, by adjusting the trim pot! using a small flathead screwdriver, you can increase (clockwise) or decrease (counter-clockwise) the threshold temperature.
Note: Ben and Baran could not get this thing to work properly. If you manage to get it functioning properly you will get a special prize.

<img
alt="Digital Temperature Sensor"
src={useBaseUrl('img/components/digital_temperature_sensor.jpeg')}
class="component-image"
/>

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
#define LED_PIN 13
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_PIN, OUTPUT);
  pinMode(6, INPUT);
}

// the loop function runs over and over again forever
void loop() {
  if(digitalRead(6) == HIGH) {
    digitalWrite(LED_PIN, HIGH);
  } else {
    digitalWrite(LED_PIN, LOW);
  }

}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Flame Sensor

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Flame Sensor"
src={useBaseUrl('img/components/flame_sensor.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
#include <Adafruit_Arcada.h>

Adafruit_Arcada arcada;

int flame_sensor = 4;
int flame_detected;

void setup()
{
  Serial.begin(9600);
  pinMode(flame_sensor, INPUT);

  arcada.displayBegin();

  for (int i=0; i<250; i+=10) {
    arcada.setBacklight(i);
    delay(1);
  }
  arcada.display->setCursor(0, 0);
  arcada.display->setTextWrap(true);
  arcada.display->setTextSize(2);
  arcada.display->setTextColor(ARCADA_WHITE, ARCADA_BLACK);

}

void loop()
{
  flame_detected = digitalRead(flame_sensor);
  if (flame_detected == 1)
  {
    Serial.println("Flame detected...! take action immediately.");
    arcada.display->print("FIRE");

  }
  else
  {
    Serial.println("No flame detected. stay cool");
    arcada.display->print("no flame ");
  }
  delay(1000);
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Hall Effect Sensor

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Hall Effect Sensor"
src={useBaseUrl('img/components/hall_effect_sensor.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Heartbeat Sensor

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Heartbeat Sensor"
src={useBaseUrl('img/components/heartbeat_sensor.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### IR Emitter

This looks like a normal LED, but the light it emits is on the infra-red spectrum. when you turn it on and don't see anything, don't panic! Humans cannot see infra-red light. Who can? The IR receiver can! Also, some cameras can pick it up, and it is used in night vision goggles. Most remotes use IR blips to communicate, so with this emitter you could emulate almost any remote!

<img
alt="IR Emitter"
src={useBaseUrl('img/components/ir_emitter.jpeg')}
class="component-image"
/>

The IR emitter has three connections -- power, ground, and S. The S pin, when high, will turn on the IR emitter. Remember that you won't be able to see any light coming out. If you want to test the IR emitter's functionality, the following codes have also incorporated the IR receiver. Make sure the receiver and the emitter are pointed at each other.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
void setup() {
  pinMode(2, OUTPUT); // pin 2 is connected to the signal pin of the IR Emitter
  digitalWrite(2, LOW);
  pinMode(4, INPUT_PULLUP); // pin 4 is the IR Receiver connection
  Serial.begin(115200);
}

void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite(2, HIGH);
  Serial.println(digitalRead(4));
  delay(100);
  digitalWrite(2, LOW);
  Serial.println(digitalRead(4));
  delay(100);
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### IR Receiver

The IR receiver is a sensor that measures IR light. You can use this in combination with the IR emitter for easy wireless communication! This emitter is similar to the one you would find in almost any remote-controlled appliance.
<img
alt="IR Receiver"
src={useBaseUrl('img/components/ir_reciever.jpeg')}
class="component-image"
/>

The code below simply demonstrates how to read data from the IR receiver. Point any remote control at the receiver and see the indicator light on the sensor blink rapidly! You can also see the signal in the serial monitor, but be quick because it happens very fast. the signal pin of the module should be connected to pin 6.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
void setup() {
  // put your setup code here, to run once:
  pinMode(6, INPUT);
  Serial.begin(115200);
}

void loop() {
  Serial.println(digitalRead(6));
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Joystick

This is a description of how to use this analog joystick!

<img
alt="Joystick"
src={useBaseUrl('img/components/joystick.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
#include <Adafruit_Arcada.h>

Adafruit_Arcada arcada;

// Arduino pin numbers
const int SW_pin = 6; // digital pin connected to switch output
const int X_pin = 0; // analog pin connected to X output - this should be the pin number on the dragontail
const int Y_pin = 1; // analog pin connected to Y output = this should be equal to the pin number on the dragontail
 
void setup() {
  pinMode(SW_pin, INPUT);
  digitalWrite(SW_pin, HIGH);
  Serial.begin(115200);

  arcada.displayBegin();

  for (int i=0; i<250; i+=10) {
    arcada.setBacklight(i);
    delay(1);
  }
  arcada.display->setCursor(0, 0);
  arcada.display->setTextWrap(true);
  arcada.display->setTextSize(2);
  arcada.display->setTextColor(ARCADA_WHITE, ARCADA_BLACK);
  
}
 
void loop() {
  
  Serial.print("Switch:  ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(X_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println(analogRead(Y_pin));
  Serial.print("\n\n");

  arcada.display->setCursor(0, 0);

  arcada.display->print("Switch: ");
  arcada.display->print(digitalRead(SW_pin));
  
  arcada.display->print(" x-axis: ");
  arcada.display->print(analogRead(X_pin));
  
  arcada.display->print(" y-axis: ");
  arcada.display->print(analogRead(Y_pin));
 
  delay(500);

}

```

</TabItem>
<TabItem value="py">

```py

# This joystick has 3 values - 1 digital for the button, and 2 analogs for the x and y directions!

import digitalio
import analogio
import board

# Set the pin number
button = digitalio.DigitalInOut(board.D6)
# Input/output
button.direction = digitalio.Direction.INPUT
# Pullup resistor
button.pull = digitalio.Pull.UP

x = analogio.AnalogIn(board.A4)
y = analogio.AnalogIn(board.A0)



while True:
  # Access the pin values with .value tag!

  print("Button value: " + button.value)
  #print(x.value)
  #print(y.value)
```

</TabItem>
</Tabs>

---

### Large Microphone

This microphone can detect sound level.
Part: HW-485

<img
alt="Large Microphone"
src={useBaseUrl('img/components/large_microphone.jpg')}
class="component-image"
/>

This microphone can work with both analog and digital inputs, but I strongly recommend that you use the analog input pin. The sample code below is done with analog input as well. In the arduino ide, open serial plotter to see the graph of outputs. With circuit python, the printing is done on the lcd. Please see the above image in order to see the pin labels.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
int soundPin = A2; // select the input pin for the microphone
int val = 0; // variable to store the value coming from the sensor

void setup ()
{
  pinMode (soundPin, INPUT);
  Serial.begin (115200); //begin the serial
}

void loop ()
{
  val = analogRead (soundPin);//read input
  delay (300);
  Serial.println (val, DEC);
}
```

</TabItem>
<TabItem value="py">

```py
import board
import time
from analogio import AnalogIn

microphone = AnalogIn(board.A2)

while True:
    print(get_voltage(photo)) #check what the voltage is and print
    time.sleep(0.1) #sleep for a 1/10th of a second
```

</TabItem>
</Tabs>

---

### Laser

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Laser"
src={useBaseUrl('img/components/laser.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Light Blocking Module

The light blocking module (HW-487) has a u-shaped component that detects whether something is blocking light from passing between the two
<img
  alt="Light Blocking Module"
  src={useBaseUrl('img/components/light_blocking_module.jpeg')}
  class="component-image"
/>

The microcontroller should treat this as a digital input device.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
int lightBlockingSensorPin = 2;
int ledPin = 14;
int lightBlockingSensorVal; // define numeric variables val
void setup ()
{
  Serial.begin(9600);
  pinMode (lightBlockingSensorPin, INPUT) ;
  pinMode (ledPin, OUTPUT) ;
}
void loop ()
{
  lightBlockingSensorVal = digitalRead (lightBlockingSensorPin) ;

  digitalWrite(ledPin, lightBlockingSensorVal);   // light up LED when no light is detected by sensor

  Serial.print("Light blocking sensor blocked?: ");
  Serial.println(lightBlockingSensorVal);
}
```

</TabItem>
<TabItem value="py">

```py
import board
import digitalio

lightBlockingSensor = digitalio.DigitalInOut(board.D2) #set light blocking sensor pin
lightBlockingSensor.direction = digitalio.Direction.INPUT

led = digitalio.DigitalInOut(board.D14) #set led pin
led.direction = digitalio.Direction.OUTPUT

while True:
  if lightBlockingSensor.value: #if light detects no light (something is blocking it)
    led.value = True; # led is on
  else: #if nothing is blocking the light blocking sensor
    led.value = False; #led is off
```

</TabItem>
</Tabs>

---

### Light Cup

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Light Cup"
src={useBaseUrl('img/components/light_cup.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Linear Hall Effect Sensor

HW-509
This sensor produces a voltage when placed in a magnetic field. In practice, it is very similar to the digital hall effect sensor (HW-492) and the analog hall effect sensor (HW-495), however, it has an both analog and digital pins.

<img
alt="Linear Hall Effect Sensor"
src={useBaseUrl("img/components/linear_hall_effect_sensor.jpeg")}
class="component-image"
/>

The linear hall effect sensor is an input device that is used to measure the presence and/or strength of a magnetic field. As labeled on the component itself and in the picture above, the pins from left to right are: Analog input, GND, VDD, Digital input.
Key things:

- This sensor can produce an analog or a digital value, as it has an ADC built-in.
- It has a built-in sensitivity adjustment (fine adjustment). This is the bronze-colored adjuster on the blue piece. You can use your fingernail or flathead screwdriver or something to adjust it. Turning the sensitivity fine adjustment **counter clockwise** makes the analog hall sensor measurement **more sensitive**, and turning it clockwise makes it less sensitive.
- It has a signal output indication. As shown in the photo below, when a magnet is held near the transistor, the built-in indication light (on the left in the photo) lights up. (This is not programmed by the user, it comes like this.)

<img
alt="Linear Hall Effect Sensor with Magnet"
src={useBaseUrl("img/components/linear_hall_effect_sensor2.jpeg")}
class="component-image"
/>

When you hold a magnet near the black transistor on the sensor (at the top of the photo), the digital reading should be 1 (HIGH). The analog sensor's reading is a numerical value that is different depending on magnet strength, sensitivity adjustment, magnet proximity, and other factors.


Note on the below CircuitPython code: [here](https://learn.adafruit.com/circuitpython-essentials/circuitpython-analog-in) are more details on reading analog input in circuitpython, including an explanation of the `get_voltage(pin)` helper function.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
int linearHallSensorDigitalPin = 8; // define linear hall sensor digital pin
int linearHallSensorAnalogPin = 2; // define linear hall sensor analog pin
//int hallSensorPin = 9;
//int buttonpin = 3; // define Metal Touch Sensor Interface
int linearHallSensorDigitalVal, linearHallSensorAnalogVal; // define numeric variables val
int lineCount = 0;  // there are 30 lines on screen for printing
void setup ()
{
  Serial.begin(9600);
  // define sensor pins as input interface
  pinMode (linearHallSensorDigitalPin, INPUT) ;
  pinMode (linearHallSensorAnalogPin, INPUT) ;
}
void loop ()
{
  linearHallSensorDigitalVal = digitalRead (linearHallSensorDigitalPin) ;
  linearHallSensorAnalogVal = analogRead (linearHallSensorAnalogPin) ;

  Serial.print("Linear hall sensor - digital: ");
  Serial.print(linearHallSensorDigitalVal);
  Serial.print(" , analog: ");
  Serial.println(linearHallSensorAnalogVal);
}
```

</TabItem>
<TabItem value="py">

```py
import board
import digitalio
import analogio

linearHallSensor_analog = analogio.AnalogIn(board.A2) #set light blocking sensor pin

linearHallSensor_digital = digitalio.DigitalInOut(board.D7)
linearHallSensor_digital.direction = digitalio.Direction.INPUT

led = digitalio.DigitalInOut(board.D14) #set led pin
led.direction = digitalio.Direction.OUTPUT

def get_voltage(pin):
  return (pin.value * 3.3) / 65536


while True:
  digitalReading = linearHallSensor_digital.value

  led.value = digitalReading  # set led based on digitalr reading of magnetic field
  print("digital:", digitalReading, "voltage:", get_voltage(linearHallSensor_analog), "V")
  ```

</TabItem>
</Tabs>

---

### Mini Reed Switch

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Mini Reed Switch"
src={useBaseUrl('img/components/mini_reed_switch.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Passive Buzzer

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Passive Buzzer"
src={useBaseUrl('img/components/passive_buzzer.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Photo Resistor

Part: HW-486
This is a photoresistor sensor, which means that it can measure the amount of ambient light!

<img
alt="Photo Resistor"
src={useBaseUrl('img/components/photo_resistor.jpg')}
class="component-image"
/>

See the image above to see the gnd, vdd, and data pins. You need to declare this as an input, and please note that you have to select an ANALOG pin and make an ANALOG measurement.
Note: The sensor is not very accurate, but should be good enough to distinguish between night and day.


Note on the below CircuitPython code: [here](https://learn.adafruit.com/circuitpython-essentials/circuitpython-analog-in) are more details on reading analog input in circuitpython, including an explanation of the `get_voltage(pin)` helper function.
<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
const int photoPin = A2; //set these as constants
int val = 0;

void setup() {
  pinMode(photoPin, INPUT); //set the photoresistor sensor as an input
  Serial.begin(9600);
}

void loop() {
  val = analogRead(photoPin);//read the value of the photoresistor
  delay(1000);
  Serial.println(val, DEC); //print on the serial monitor
}
```

</TabItem>
<TabItem value="py">

```py
import board
import time
from analogio import AnalogIn

photo = AnalogIn(board.A2)

def convertToVoltage(pin):
    return (pin.value * 3) / 65536 #convert it to a voltage value between 0-3V


while True:
    print((get_voltage(photo),)) #check what the voltage is- if the voltage is higher, it is brighter
    time.sleep(1) #sleep for a second
```

</TabItem>
</Tabs>

---

### RGB LED

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="RGB LED"
src={useBaseUrl('img/components/rgb_led.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Reed Switch

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Reed Switch"
src={useBaseUrl('img/components/reed_switch.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Relay

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Relay"
src={useBaseUrl('img/components/relay.jpeg')}
class="component-image"
/>

The relay module is an effective way to convert existing appliances into smart-objects. The relay is a heavy-duty, digitally controlled switch that can handle anything from battery power to wall current. The relay has 3 control pins (+V, Gnd, and Signal) and three screw terminals (NC, common, NO). When no voltage is applied to the relay, the NC (Normally Closed) terminal and the common (middle) terminals are connected. When a logical high voltage is applied to the signal pin, an electromagnet removes the NC-Common connection and connects the common and NO (normally open) terminals. You could, for example, splice the the power cord running to your toaster -- BOOM SMART TOASTER!
DISCLAIMER: do NOT splice any power cords running high voltage or current!! Getting zapped by an improperly shielded power cable can KILL you. It can also start fires. Consult with an expert before modifying any existing power cords. This module can be used effectively in low-power applications as well!

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
void setup() {
  // put your setup code here, to run once:
  pinMode(2, OUTPUT); // pin 2 is connected to the signal pin of the relay
  digitalWrite(2, LOW);
  pinMode(5, INPUT_PULLUP); // pin 5 is the left-hand Clue button
}

short relay_state = 0;
void loop() {
  // put your main code here, to run repeatedly:
  if(!digitalRead(5)) {
    if(!relay_state) relay_state = 1;
    else relay_state = 0;
    delay(200); //EZ debounce
  }
  if(relay_state) digitalWrite(2, HIGH);
  else digitalWrite(2, LOW);
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Rotary Encoder

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Rotary Encoder"
src={useBaseUrl('img/components/rotary_encoder.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### SMD RGB

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="SMD RGB"
src={useBaseUrl('img/components/smd_rgb.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Shock Sensor

Part Number: HW-513

<img
alt="Shock Sensor"
src={useBaseUrl('img/components/shock_sensor.jpg')}
class="component-image"
/>

As you can see in the above image, the left-most pin is gnd, the center pin is power, and the right pin is data. This sensor is an input, and can detect "shocks". You can apply shock to this sensor by dropping it or hitting the blue part lightly with your finger.
Note: A low read from the sensor means it detected a shock.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
const int shockPin = 1; //set these as constants
int val = 0;

void setup() {
  pinMode(LED_BUILTIN, OUTPUT); //using the inbuilt LED on the back of the clue!
  pinMode(shockPin, INPUT); //set the shock sensor as an input
}

void loop() {
  val = digitalRead(shockPin);//read the state of the button

  if (val == LOW) { //if a shock is detected
    //turn LED on
    digitalWrite(LED_BUILTIN, HIGH);
    delay(1000); //delay
  } else { //if the shock is not detected
    // turn LED off:
    digitalWrite(LED_BUILTIN, LOW);
  }
}
```

</TabItem>
<TabItem value="py">

```py
import board
import digitalio
import time

led = digitalio.DigitalInOut(board.D7) #set led pin
shock = digitalio.DigitalInOut(board.D1) #set shock pin
led.direction = digitalio.Direction.OUTPUT
shock.direction = digitalio.Direction.INPUT

while True:
  if shock.value: #if the shock is not detected
    led.value = False; #led is off
  else: #if the shock is detected
    led.value = True; #led is on
    time.sleep(1); #delay so you can see the led light
```

</TabItem>
</Tabs>

---

### Small Microphone

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Small Microphone"
src={useBaseUrl('img/components/small_microphone.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### TEMP 18B20 Sensor

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="TEMP 18B20 Sensor"
src={useBaseUrl('img/components/temp_18b20_sensor.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Tap Module

The knock sensor (tap module) is a very simple way to detect knocks or other impacts. It's a very simple design -- there's a spring in a tube that, when shaken, 
taps against a contact that completes a circuit from the signal pin to ground. The spring is fairly stiff, so a good *thwack* with a pen will register pretty cleanly as a single knock. You could use this to add knock controls to your latest gadget, or even embed it in your desk to be triggered when you rage slam your keyboard!

<img
alt="Tap Module"
src={useBaseUrl('img/components/tap_module.jpeg')}
class="component-image"
/>

Wire the - pin to ground, the middle (+) pin to 3V, and the S pin to an input pin on your Clue. I used pin 4 for the example. Below is an example sketch that registers any knocks to the serial port.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
void setup() {
  pinMode(4, INPUT); //connect the knock sensor signal to pin 4
  Serial.begin(115200); //open your serial monitor to 115200 baud
}

void loop() {
  // if the knock sensor signal goes low, wwe have been knocked!
  if(!digitalRead(4)) Serial.println("KNOCK");
  delay(1);
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import time
from digitalio import DigitalInOut, Direction, Pull
from adafruit_clue import clue



# initialize pin 4 as an input with a pullup resistor
knock_sensor = DigitalInOut(board.D4)
knock_sensor.direction = Direction.INPUT
knock_sensor.pull = Pull.UP

# define a simple function to turn an onboard LED on or off each call
# be warned: these things are BRIGHT
def toggle_LED():
    if clue.white_leds:
        clue.white_leds = False
    else:
        clue.white_leds = True


# Loop forever
while True:
    if not knock_sensor.value:
        print("knock")
        toggle_LED() 
        time.sleep(.1)


```

</TabItem>
</Tabs>

---

### Temperature and Humidity Sensor

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Temperature and Humidity Sensor"
src={useBaseUrl('img/components/temperature_and_humidity_sensor.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Tilt Switch

This tilt switch will be able to detect whether is tilting to the right or the left.
Part: HW-505

<img
alt="Tilt Switch"
src={useBaseUrl('img/components/tilt_switch.jpeg')}
class="component-image"
/>

Please see the above image to see where the vdd, gnd, and data pins are. The tilt sensor is used as a digital input, and if the bead of mercury is tilted towards the base, then the led on the sensor will flash. If the bead of mercury is tilted away from the base, then the led on the sensor will turn off.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
const int tiltPin = 2; //set these as constants
int val = 0;

void setup() {
  pinMode(LED_BUILTIN, OUTPUT); //using the inbuilt LED on the back of the clue!
  pinMode(tiltPin, INPUT); //set the shock sensor as an input
}

void loop() {
  val = digitalRead (tiltPin) ;// read the values assigned to the digital interface 3 val
  if (val == HIGH) // When the mercury tilt switch sensor detects a signal, LED flashes
  {
    digitalWrite (LED_BUILTIN, HIGH);
  }
  else
  {
    digitalWrite (LED_BUILTIN, LOW);
  }
}
```

</TabItem>
<TabItem value="py">

```py
import board
import digitalio
import time

tilt = digitalio.DigitalInOut(board.D2) #set tilt sensor pin
tilt.direction = digitalio.Direction.INPUT

led = digitalio.DigitalInOut(board.D7) #set led pin
led.direction = digitalio.Direction.OUTPUT

while True:
  if tilt.value: #if the tilt sensor is tilted towards the base
    led.value = True; #led is off
  else: #if the tilt sensor is tilted away from the base
    led.value = False; #led is on
```

</TabItem>
</Tabs>

---

### Touch Sensor

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Touch Sensor"
src={useBaseUrl('img/components/touch_sensor.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Tracking Sensor

This is a sensor that can detect if the object in front of the white circle is black or white. You can use this to make a robot car follow a straight line!
Part: HW-511

<img
alt="Tracking Sensor"
src={useBaseUrl('img/components/tracking_sensor.jpg')}
class="component-image"
/>

Please see the above image to see where the data, gnd, and vdd pins are. If you are testing this code using the arduino IDE, open the serial monitor to see if it is correctly detecting whether the object in front of it is black or white. If you are using circuit python, make sure to look at the lcd display.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
const int trackPin = 2; //set these as constants
int val = 0;

void setup() {
  Serial.begin(9600); //start serial
  pinMode(trackPin, INPUT); //set the tracking sensor as an input
}

void loop() {
  val = digitalRead (trackPin) ;// read the values of the tracking sensor
  Serial.println(val);
  delay(500); //delay so you don't spam the serial console
}


```

</TabItem>
<TabItem value="py">

```py
import board
import digitalio
import time

track = digitalio.DigitalInOut(board.D2) #set track sensor pin
track.direction = digitalio.Direction.INPUT

while True:
  print(track.value); #print either a 0 or 1
  sleep(1); # delay for a second

```

</TabItem>
</Tabs>

---

### Two-color LED

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Two-color LED"
src={useBaseUrl('img/components/two-color_led.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>

---

### Two-color LED 2

This is a description about what the module is/does so that people will know what they can use it for!

<img
alt="Two-color LED 2"
src={useBaseUrl('img/components/two-color_led_2.jpeg')}
class="component-image"
/>

Now explain everything about how to use the module. This will include how the pins should be connected,
whether the microcontroller should be treating this an output or input, digital or analog, or if it should be something else entirely.

<Tabs
defaultValue="arduino"
values={[
{ label: 'Arduino', value: 'arduino', },
{ label: 'CircuitPython', value: 'py', },
]
}>
<TabItem value="arduino">

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(500);                // wait for half a second
}
```

</TabItem>
<TabItem value="py">

```py
# Import all of the necessary modules.
import board
import digitalio
import time

# Initialize digital pin 17 as an output.
led = digitalio.DigitalInOut(board.D17)
led.direction = digitalio.Direction.OUTPUT

# Loop forever
while True:
    led.value = True    # Turn LED on
    time.sleep(0.5)     # Wait half a second
    led.value = False   # Turn LED off
    time.sleep(0.5)     # Wait half a second
```

</TabItem>
</Tabs>
