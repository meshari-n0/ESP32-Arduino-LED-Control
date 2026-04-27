# ESP32 & Arduino LED Control

## Overview
This project connects an ESP32 with an Arduino Uno using UART communication.

The ESP32 sends commands to the Arduino, and the Arduino controls an LED.

## Project Idea
- ESP32 sends `1` to turn the LED ON.
- ESP32 sends `0` to turn the LED OFF.
- Arduino receives the command and controls the LED.

## Components
- ESP32
- Arduino Uno
- LED
- Breadboard
- Jumper wires

## Connection

### ESP32 to Arduino
| ESP32 | Arduino Uno |
|---|---|
| GPIO17 / TX | Pin 10 |
| GND | GND |

### LED to Arduino
| Arduino Uno | LED |
|---|---|
| Pin 8 | Long leg of LED |
| GND | Short leg of LED |


## Arduino Code
```cpp
#include <SoftwareSerial.h>

SoftwareSerial mySerial(10, 11);
int led = 8;

void setup() {
  pinMode(led, OUTPUT);
  mySerial.begin(9600);
}

void loop() {
  if (mySerial.available()) {
    char x = mySerial.read();

    if (x == '1') digitalWrite(led, HIGH);
    if (x == '0') digitalWrite(led, LOW);
  }
}
```
## ESP32 Code
```cpp

HardwareSerial MySerial(2);

void setup() {
  MySerial.begin(9600, SERIAL_8N1, 16, 17);
}

void loop() {
  MySerial.write('1');
  delay(2000);
  MySerial.write('0');
  delay(2000);
}
