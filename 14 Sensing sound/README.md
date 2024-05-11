126. [Introduction to sensing sound](#126)
127. [Introduction to the analog sound sensor](#127)
128. [A demonstration and sketch of the analog sound sensor](#128)
129. [A demonstration and sketch of the digital sound sensor](#129)

---

### 126. Introduction to sensing sound<a id="126"></a>

### 127. Introduction to the analog sound sensor<a id="127"></a>

- Wiki Signal processing topic [click me](https://en.wikipedia.org/wiki/Signal_processing)

### 128. A demonstration and sketch of the analog sound sensor<a id="128"></a>

- Wiki Loudness concept [click me](https://en.wikipedia.org/wiki/Loudness)

- Wiki Audio signal processing topic [click me](https://en.wikipedia.org/wiki/Audio_signal_processing)

```ino
/*  Analog microphone demo sketch
 *
 * This sketch detects loud noises using an analog electrelet microphone.
 *
 * This sketch was written for Arduino Step by Step by Peter Dalmaris.
 *
 * Components
 * ----------
 *  - Arduino Uno
 *  - Analog electrelet microphone
 *
 *  Libraries
 *  ---------
 *  - None
 *
 * Connections
 * -----------
 *  Break out    |    Arduino Uno
 *  -----------------------------
 *      VCC      |      5V
 *      GND      |      GND
 *      AUD      |      A0

 *
 * Other information
 * -----------------
 *  This code is useful if you want to do things like detect a knock on a door,
 *  hands clapping, etc.
 *
 *  Created on October 14 2016 by Peter Dalmaris
 *
 */

int currentValue;
int maxValue;
int minValue;
unsigned long timer;
int sampleSpan  = 200; // Amount in milliseconds to sample data
int volume;            // this roughly goes from 0 to 700
int ledpin      = 7;

void setup()
{
    Serial.begin(9600);
    pinMode (ledpin, OUTPUT);
    resetValues();
}

void loop()
{
    currentValue = analogRead(A0);

    if (currentValue < minValue) {
        minValue = currentValue;
    }
    if (currentValue > maxValue) {
        maxValue = currentValue;
    }

    if (millis() - timer >= sampleSpan) {
        volume = maxValue - minValue;
        //Serial.println(volume);
        resetValues();
    }

    // I arbitrarily select 100 as the value above which the
    //microphone is picking a loud noise.
    if (volume > 400)
    {
      Serial.println("Loud");
      digitalWrite(ledpin,HIGH);
    } else
    {
      Serial.println("Quiet");
      digitalWrite(7,LOW);
    }

}

void resetValues()
{
    maxValue = 0;
    minValue = 1024;
    timer = millis();
}
```

### 129. A demonstration and sketch of the digital sound sensor<a id="129"></a>

<img src="assets/images/45.png" width="700">
- github Adafruit_BMP085_Unified [click me](Adafruit_BMP085_Unified)
- Ardunio uno r3 documentation #define [click me](https://www.arduino.cc/reference/en/language/structure/further-syntax/define/)
- Wiki Gamma correction concept [click me](https://en.wikipedia.org/wiki/Gamma_correction)
- BMP180 digital pressure sensor datasheet [click me](https://www.digikey.com/htmldatasheets/production/856385/0/0/1/bmp180-datasheet.html)
