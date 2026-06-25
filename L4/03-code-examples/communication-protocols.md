# Communication Protocols — I2C, SPI, UART

> *通訊協定* | Mechatronics must-know

---

## 1. UART — Serial Communication（串口通訊）

Already covered in Serial Monitor. For Arduino-to-Arduino:

```cpp
// Sender（發送端）
void setup() { Serial2.begin(9600, SERIAL_8N1, 16, 17); } // RX=16, TX=17
void loop() { Serial2.println("Hello from ESP32!"); delay(1000); }

// Receiver（接收端）
void setup() { Serial2.begin(9600, SERIAL_8N1, 16, 17); Serial.begin(115200); }
void loop() {
  if (Serial2.available()) {
    String msg = Serial2.readStringUntil('\n');
    Serial.println("Received: " + msg);
  }
}
```

ESP32 has 3 hardware UARTs: Serial (USB), Serial1, Serial2.

---

## 2. I2C — LCD 1602 Display（I2C LCD 1602 顯示器）

**Wiring**: SDA → GPIO 21, SCL → GPIO 22

```cpp
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);  // Address 0x27, 16 cols, 2 rows

void setup() {
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("Mechatronic");
  lcd.setCursor(0, 1);
  lcd.print("MC 091-03-2016");
}

void loop() {
  // Scroll text（滾動文字）
  for (int i = 0; i < 16; i++) {
    lcd.scrollDisplayLeft();
    delay(300);
  }
}
```

---

## 3. I2C Scanner — Find Device Address（掃描 I2C 設備）

```cpp
#include <Wire.h>

void setup() {
  Serial.begin(115200);
  Wire.begin();  // SDA=21, SCL=22 (ESP32 default)
  Serial.println("I2C Scanner...");
}

void loop() {
  byte count = 0;
  for (byte addr = 1; addr < 127; addr++) {
    Wire.beginTransmission(addr);
    if (Wire.endTransmission() == 0) {
      Serial.print("Device at 0x");
      Serial.println(addr, HEX);
      count++;
    }
  }
  Serial.print("Found "); Serial.print(count); Serial.println(" device(s)");
  delay(5000);
}
```

---

## 4. I2C — Multiple Sensors（多感測器）

```cpp
// BME280 Temperature + Humidity + Pressure
#include <Adafruit_BME280.h>
Adafruit_BME280 bme;

void setup() {
  Serial.begin(115200);
  if (!bme.begin(0x76)) {  // 0x76 or 0x77
    Serial.println("BME280 not found!");
  }
}

void loop() {
  Serial.print("Temp: "); Serial.print(bme.readTemperature()); Serial.print("°C  ");
  Serial.print("Humidity: "); Serial.print(bme.readHumidity()); Serial.print("%  ");
  Serial.print("Pressure: "); Serial.print(bme.readPressure() / 100.0); Serial.println("hPa");
  delay(2000);
}
```

---

## 5. SPI — Basic Structure（SPI 基本結構）

ESP32 default SPI: MOSI=23, MISO=19, SCK=18, SS=5

```cpp
#include <SPI.h>

const int ssPin = 5;

void setup() {
  Serial.begin(115200);
  SPI.begin();  // Default SPI pins
  pinMode(ssPin, OUTPUT);
  digitalWrite(ssPin, HIGH);
}

void loop() {
  digitalWrite(ssPin, LOW);    // Select device
  SPI.transfer(0x42);          // Send byte, receive response
  digitalWrite(ssPin, HIGH);   // Deselect device
  delay(100);
}
```

---

## Protocol Comparison（通訊協定比較）

| Feature | UART | I2C | SPI |
|---|---|---|---|
| Wires | 2 (RX+TX) | 2 (SDA+SCL) | 4 (MOSI+MISO+SCK+SS) |
| Speed | Up to ~1Mbps | 100k/400k/1M | Up to 80MHz |
| Devices | 1-to-1 | Up to 127 | Limited by SS pins |
| Distance | Long (meters) | Short (PCB) | Very short |
| Complexity | Simplest | Address-based | Fastest |
| Use Case | GPS, Bluetooth, PC | LCD, sensors, RTC | SD cards, displays, fast ADCs |

---

## ESP32 Default Pins

| Protocol | Default Pins |
|---|---|
| I2C | SDA=21, SCL=22 |
| SPI (VSPI) | MOSI=23, MISO=19, SCK=18, SS=5 |
| UART0 (USB) | RX=3, TX=1 |
| UART2 | RX=16, TX=17 |
