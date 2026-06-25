# Digital I/O — Code Examples

> *數位輸入輸出* | Ready-to-use snippets
> Commands: `digitalWrite`, `digitalRead`, `pinMode`

---

## 1. Single LED Blink（單顆 LED 閃爍）

```cpp
const int led = 2;

void setup() { pinMode(led, OUTPUT); }

void loop() {
  digitalWrite(led, HIGH); delay(500);
  digitalWrite(led, LOW);  delay(500);
}
```

---

## 2. Multiple LEDs — Chase Light（跑馬燈）

```cpp
const int leds[] = {2, 4, 5, 12, 13};
const int numLeds = 5;

void setup() {
  for (int i = 0; i < numLeds; i++)
    pinMode(leds[i], OUTPUT);
}

void loop() {
  for (int i = 0; i < numLeds; i++) {
    digitalWrite(leds[i], HIGH); delay(100);
    digitalWrite(leds[i], LOW);
  }
}
```

---

## 3. Button Toggle LED（按鈕切換 LED）

```cpp
const int btn = 15, led = 2;
bool state = false;
int lastBtn = HIGH;

void setup() {
  pinMode(led, OUTPUT);
  pinMode(btn, INPUT_PULLUP);
}

void loop() {
  int reading = digitalRead(btn);
  if (reading == LOW && lastBtn == HIGH) { // Falling edge
    state = !state;
    digitalWrite(led, state);
    delay(50); // debounce
  }
  lastBtn = reading;
}
```

---

## 4. Button Hold to Light（按住才亮）

```cpp
const int btn = 15, led = 2;

void setup() {
  pinMode(led, OUTPUT);
  pinMode(btn, INPUT_PULLUP);
}

void loop() {
  digitalWrite(led, !digitalRead(btn)); // LOW=pressed → HIGH=ON
}
```

---

## 5. Traffic Light System（交通燈系統）

```cpp
const int red = 13, yellow = 12, green = 14;

void setup() {
  pinMode(red, OUTPUT); pinMode(yellow, OUTPUT); pinMode(green, OUTPUT);
}

void loop() {
  // Green 5s → Yellow 2s → Red 5s
  digitalWrite(green, HIGH);  delay(5000); digitalWrite(green, LOW);
  digitalWrite(yellow, HIGH); delay(2000); digitalWrite(yellow, LOW);
  digitalWrite(red, HIGH);    delay(5000); digitalWrite(red, LOW);
}
```

---

## 6. State Machine — Single Click vs Double Click

```cpp
const int btn = 15, led = 2;
unsigned long lastPress = 0;
int clickCount = 0;

void setup() {
  pinMode(led, OUTPUT); pinMode(btn, INPUT_PULLUP);
  Serial.begin(115200);
}

void loop() {
  if (digitalRead(btn) == LOW) {
    clickCount++;
    lastPress = millis();
    delay(200); // debounce
  }

  if (clickCount > 0 && (millis() - lastPress > 400)) {
    if (clickCount == 1) Serial.println("Single click!");
    if (clickCount == 2) Serial.println("Double click!");
    clickCount = 0;
  }
}
```

---

## Quick Reference（速查）

| Pattern | Code |
|---|---|
| Read button (INPUT_PULLUP) | `if (digitalRead(pin) == LOW)` — pressed |
| Toggle | `state = !state; digitalWrite(pin, state);` |
| Debounce | `delay(50);` or use `millis()` timing |
| Rising edge detect | `if (now == HIGH && last == LOW)` |
| Falling edge detect | `if (now == LOW && last == HIGH)` |
| Blink without delay | Use `millis()` instead of `delay()` |
