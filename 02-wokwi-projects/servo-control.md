# Servo Motor Control — Wokwi Project

> *Servo 馬達控制* | Copy & Run in Wokwi
> **Skill**: PWM, Servo library, angle control

---

## Wiring（接線）

In Wokwi, add **Servo Motor** from the `+` menu:

| Servo Wire | ESP32 Pin |
|---|---|
| Orange (Signal) | GPIO **13** |
| Red (VCC / 5V) | **5V** |
| Brown (GND) | **GND** |

---

## Code（程式碼）

```cpp
#include <ESP32Servo.h>

Servo myServo;
const int servoPin = 13;

int angle = 0;
int step = 2;          // 2° per step = smooth
bool increasing = true;

void setup() {
  Serial.begin(115200);
  myServo.attach(servoPin);
  Serial.println("=== Servo 0° ~ 180° Scan ===");
}

void loop() {
  myServo.write(angle);
  Serial.printf("Angle: %d°\n", angle);

  if (increasing) {
    angle += step;
    if (angle >= 180) { angle = 180; increasing = false; }
  } else {
    angle -= step;
    if (angle <= 0)   { angle = 0;   increasing = true;  }
  }
  delay(30);
}
```

---

## diagram.json Config（接線配置）

```json
{
  "version": 1,
  "parts": [
    { "type": "wokwi-servo", "id": "servo1", "top": 0, "left": 200, "attrs": {} }
  ],
  "connections": [
    ["servo1:V+", "$5V", "red", []],
    ["servo1:V-", "$GND", "black", []],
    ["servo1:GPWM", "board1:13", "orange", []]
  ]
}
```

---

## What You See（效果）

- Servo rotates 0° → 180° → 0° continuously
- Serial Monitor prints current angle
- ~4.5 seconds per full sweep

---

## How It Works（原理）

| Line | Explanation |
|---|---|
| `#include <ESP32Servo.h>` | Load Servo library |
| `Servo myServo;` | Create a Servo object |
| `myServo.attach(13);` | Bind Servo to GPIO 13 |
| `myServo.write(angle);` | Move to angle (0°–180°) |
| `Serial.printf(...)` | Print formatted text (like C printf) |

Set `step = 5` for faster, `step = 1` for ultra-smooth.

---

## Next Challenges（進階挑戰）

| Project | What You Learn |
|---|---|
| Potentiometer controls Servo angle | ADC + PWM together |
| Two buttons: left / right rotation | GPIO input + servo |
| Ultrasonic sensor triggers Servo | Sensor fusion |
| WiFi webpage slider controls Servo | IoT + servo |
