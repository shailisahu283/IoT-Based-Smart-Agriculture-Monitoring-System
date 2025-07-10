#**“IoT-Based Smart Agriculture Monitoring System”**

---

## 📝 Project Description:

This project monitors critical environmental parameters in agricultural fields using sensors and displays real-time data such as **soil moisture**, **temperature**, and **humidity** on an **LCD screen**. The system can also trigger automated actions like turning on a **water pump** when the soil is dry.

It simulates how **IoT can optimize irrigation and crop health**, making agriculture more efficient and sustainable.

---

## 🧰 Components Required (All work in Tinkercad):

| Component                 | Function                             |
| ------------------------- | ------------------------------------ |
| Arduino Uno               | Main controller                      |
| Soil Moisture Sensor      | Detects soil wetness/dryness         |
| DHT11 Sensor              | Measures temperature & humidity      |
| LCD 16x2 Display          | Shows real-time sensor readings      |
| Relay Module (or LED)     | Controls pump (or shows pump ON/OFF) |
| Buzzer (optional)         | Alerts when soil is too dry          |
| Potentiometer             | LCD contrast                         |
| Jumper Wires + Breadboard | Connections                          |

---

## 🔧 Circuit Design (Basic Logic):

* **Soil Moisture Sensor → A0**
* **DHT11 Sensor → D6**
* **LCD (RS-E-D4-D7) → D12, D11, D5, D4, D3, D2**
* **Relay (or LED) → D7**
* **Buzzer (optional) → D8**

---

## ✅ Code Sample (Simplified Version):

```cpp
#include <LiquidCrystal.h>
#include <DHT.h>

#define DHTPIN 6
#define DHTTYPE DHT11
#define SOIL A0
#define PUMP 7

DHT dht(DHTPIN, DHTTYPE);
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  pinMode(SOIL, INPUT);
  pinMode(PUMP, OUTPUT);
  lcd.begin(16, 2);
  dht.begin();
}

void loop() {
  int soil = analogRead(SOIL);
  float temp = dht.readTemperature();
  float hum = dht.readHumidity();

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("T:");
  lcd.print(temp);
  lcd.print(" H:");
  lcd.print(hum);

  lcd.setCursor(0, 1);
  lcd.print("Soil: ");
  lcd.print(soil);

  if (soil < 500) {
    digitalWrite(PUMP, HIGH); // Soil dry, turn ON pump
    lcd.print(" DRY");
  } else {
    digitalWrite(PUMP, LOW); // Soil wet
    lcd.print(" WET");
  }

  delay(2000);
}
```

---

## ✅ Output Example (LCD):

```
T:28.5 H:65.0
Soil: 460 DRY
```

---

## 💡 Optional Smart Features:

* Send sensor data to **Blynk or ThingSpeak** (IoT dashboard)
* Log data with **SD card module**
* Add **solar power** simulation
* Control irrigation remotely via mobile app

