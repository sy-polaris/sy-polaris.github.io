---
id: 2302
title: Sistema di controllo della temperatura dei gas di scarico 2 (Arduino)
date: 2016-09-14T18:19:35+02:00
author: polaris
layout: post
categories:
  - Senza categoria
---
**Sistema di controllo della temperatura dei gas di scarico:**

* Arduino UNO/Duemilanove
* sensore di temperatura DS18B20 stagno
* LCD display 2&#215;16 HITACHI HDD44780

![Exhaust](/foto/exhaust.jpg)

**[soglia di allarme a 85 C (come sensore Volvo)]**


Sketch Arduino

/* collegamenti DS18B20

pin 1 GND NERO

pin 3 5V ROSSO

pin 2 Arduino DIGITAL 2 GIALLO
resistenza da 10k tra 5V e pin 2

LCD ARDUINO
pin 1 GND
pin 2 5V
pin 3 centrale potenziometro
pin 4 DIGITAL 7
pin 5 GND
pin 6 DIGITAL 8
pin 7,8,9,10 non collegati
pin 11 DIGITAL 9
pin 12 DIGITAL 10
pin 13 DIGITAL 11
pin 14 DIGITAL 12
pin 15 5V
pin 16 GND
*/

#include <OneWire.h>
#include <DallasTemperature.h>

// Data wire is plugged into pin 2 on the Arduino
#define ONE\_WIRE\_BUS 2

// Setup a oneWire instance to communicate with any OneWire devices
// (not just Maxim/Dallas temperature ICs)
OneWire oneWire(ONE\_WIRE\_BUS);

// Pass our oneWire reference to Dallas Temperature.
DallasTemperature sensors(&oneWire);

/*
LiquidCrystal Library
The LiquidCrystal
library works with all LCD displays that are compatible with the
Hitachi HD44780 driver.
*/

// include the library code:
#include <LiquidCrystal.h>

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(7, 8, 9, 10, 11, 12);

void setup() {
sensors.begin();
Serial.begin(9600);
lcd.begin(16, 2);
// Print a message to the LCD.
lcd.print(&#8220;Exhaust temp: &#8220;);
}

void loop(void) {
sensors.requestTemperatures(); // Send the command to get temperatures
lcd.setCursor(14, 1);
lcd.print(sensors.getTempCByIndex(0));
// Serial.println(sensors.getTempCByIndex(0));
}
