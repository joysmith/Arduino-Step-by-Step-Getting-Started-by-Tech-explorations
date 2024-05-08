93. [Introduction to environment sensors](#93)
94. [Using a DHT22 sensor to measure temperature and humidity](#94)
95. [An introduction to the Thermistor](#95)
96. [Wiring the Thermistor](#96)
97. [How to calculate the temperature from the thermistor resistance](#97)
98. [Thermistor: getting a temperature using a library](#98)
99. [Thermistor: improving the accuracy of analog readings with AREF](#99)
100.  [An introduction to measuring temperature with the TMP36](#100)
101.  [Wiring the TMP36 and a demonstration sketch](#101)
102.  [An alternate wiring of the TMP36](#102)
103.  [An introduction to the MCP9808 for very accurate temperature readings](#103)
104.  [MCP9808: Wiring](#104)
105.  [Using the MCP9808, demo and sketch walkthrough](#105)
106.  [MCP9808: A closer look at I2C addressing](#106)
107.  [An introduction to measuring barometric pressure with the BMP180](#107)
108.  [Wiring the BMP180 and first sketch walkthrough](#108)
109.  [A first demo sketch for the BMP180](#109)
110.  [A second demo sketch for the BMP180](#110)

---

### 93. Introduction to environment sensors<a id="93"></a>

### 94. Using a DHT22 sensor to measure temperature and humidity<a id="94"></a>

Schematic

<img src="assets/images/DHT22 schematic.png.png" width="700">

- DHT22 humidity & temperature analog sensor datasheet [click me](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf)
- Wiki humidity concept [click me](https://en.wikipedia.org/wiki/Humidity#Relative_humidity)
- Wiki heat index concept [click me](https://en.wikipedia.org/wiki/Heat_index)
- Techexploration pull-up & pull-down concept [click me](https://techexplorations.com/guides/arduino/common-circuits/pull-up-and-pull-down-resistors/)
- github DHT22 library [click me](https://github.com/adafruit/DHT-sensor-library)

```ino
/*  DHT22/11 temerature and humidity sensor demonstration sketch
 *
 * This sketch reads the temperature and humidity from a DHT sensor.
 *
 * This is a common digital sensor which is calibrated in factory
 * and outputs true values so that no further calculations are needed
 * on the Arduino.

 *
 * This sketch was adapted for Arduino Step by Step by Peter Dalmaris from the
 * demo sketch that ships with the Adafruit library.
 *
 * Components
 * ----------
 *  - Arduino Uno
 *  - A DHT22 or DHT11 sensor
 *  - 10 kOhm resistor to pull up the data pin
 *
 *  Libraries
 *  ---------
 *  DHT.h
 *
 * Connections
 * -----------
 *
 * Hold the sensor so that the grill is towards you. Here are the connections
 *
 *     -----------
 *     | - |  -  |
 *     | - |  -  |
 *     | - |  -  |
 *     | - |  -  |
 *     -----------
 *     |  |  |  |
 *     |  |  |  |
 *     |  |  |  |
 *     |  |  |  |
 *    5V  2     GND
 *      data
 *
 * Connect a 10KOhm resistor between the 5V and data pin (2)
 *
 * Other information
 * -----------------
 *
 * DHT22 datasheet: https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf
 * The Github repository for the library: https://github.com/adafruit/DHT-sensor-library
 * The DHT library requires Adafruit's Unified Sensor Driver. Install that by searching
 * for "Adafruit Unified Sensor" in the Library Manager.
 * Learn more about the Unified Driver: https://github.com/adafruit/Adafruit_Sensor
 * About the Heat Index:
 * About pull up and pull down resistors:
 *
 *
 *
 *  Created on October 11 2016 by Peter Dalmaris
 *
 */

// Example testing sketch for various DHT humidity/temperature sensors
// Written by ladyada, public domain

#include "DHT.h"

#define DHTPIN 2     // what digital pin we're connected to

// Uncomment whatever type you're using!
//#define DHTTYPE DHT11   // DHT 11
#define DHTTYPE DHT22   // DHT 22  (AM2302), AM2321
//#define DHTTYPE DHT21   // DHT 21 (AM2301)

// Initialize DHT sensor.
// Note that older versions of this library took an optional third parameter to
// tweak the timings for faster processors.  This parameter is no longer needed
// as the current DHT reading algorithm adjusts itself to work on faster procs.
DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  Serial.println("DHTxx test!");

  dht.begin();
}

void loop() {
  // Wait a few seconds between measurements.
  delay(2000);

  // Reading temperature or humidity takes about 250 milliseconds!
  // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
  float h = dht.readHumidity();
  // Read temperature as Celsius (the default)
  float t = dht.readTemperature();
  // Read temperature as Fahrenheit (isFahrenheit = true)
  float f = dht.readTemperature(true);

  // Check if any reads failed and exit early (to try again).
  if (isnan(h) || isnan(t) || isnan(f)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  // Compute heat index in Fahrenheit (the default)
  float hif = dht.computeHeatIndex(f, h);
  // Compute heat index in Celsius (isFahreheit = false)
  float hic = dht.computeHeatIndex(t, h, false);

  Serial.print("Humidity: ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.print(" *C ");
  Serial.print(f);
  Serial.print(" *F\t");
  Serial.print("Heat index: ");
  Serial.print(hic);
  Serial.print(" *C ");
  Serial.print(hif);
  Serial.println(" *F");
}
```

### 95. An introduction to the Thermistor<a id="95"></a>

### 96. Wiring the Thermistor<a id="96"></a>

### 97. How to calculate the temperature from the thermistor resistance<a id="97"></a>

### 98. Thermistor: getting a temperature using a library<a id="98"></a>

### 99. Thermistor: improving the accuracy of analog readings with AREF<a id="99"></a>

### 100. An introduction to measuring temperature with the TMP36<a id="100"></a>

### 101. Wiring the TMP36 and a demonstration sketch<a id="101"></a>

### 102. An alternate wiring of the TMP36<a id="102"></a>

### 103. An introduction to the MCP9808 for very accurate temperature readings<a id="103"></a>

### 104. MCP9808: Wiring<a id="104"></a>

### 105. Using the MCP9808, demo and sketch walkthrough<a id="105"></a>

### 106. MCP9808: A closer look at I2C addressing<a id="106"></a>

### 107. An introduction to measuring barometric pressure with the BMP180<a id="107"></a>

### 108. Wiring the BMP180 and first sketch walkthrough<a id="108"></a>

### 109. A first demo sketch for the BMP180<a id="109"></a>

### 110. A second demo sketch for the BMP180<a id="110"></a>

<img src="assets/images/45.png" width="700">
- Ardunio uno r3 documentation #define [click me](https://www.arduino.cc/reference/en/language/structure/further-syntax/define/)
- Wiki Gamma correction concept [click me](<https://en.wikipedia.org/wiki/Gamma_correction>)
