# Aduino

```cpp
int pinLED[4] = {8, 9, 10, 11};
int k;

void setup() {
  Serial.begin(9600);

  for (k = 0; k < 4; k++) {
    pinMode(pinLED[k], OUTPUT);
  }

  Serial.println("Enter 1, 2, 3, 4 !");
}

void loop() {
  if (Serial.available()) {
    char select = Serial.read();

    Serial.print("Select Number = ");
    Serial.println(select);

    int select2 = select - '0';

    switch (select2) {
      case 1:
        digitalWrite(pinLED[0], HIGH);
        break;

      case 2:
        digitalWrite(pinLED[1], HIGH);
        break;

      case 3:
        digitalWrite(pinLED[2], HIGH);
        break;

      case 4:
        digitalWrite(pinLED[3], HIGH);
        break;

      default:
        for (k = 0; k < 4; k++) {
          digitalWrite(pinLED[k], LOW);
        }
        break;
    }
  }
}

```
----

```cpp
int pinSW[4] = {0, 1, 2, 3};       // 스위치
int pinLED[4] = {4, 5, 6, 7};      // LED  

void setup() {
  for (int i = 0; i < 4; i++) {
    pinMode(pinSW[i], INPUT);
    pinMode(pinLED[i], OUTPUT);
  }
}

void loop() {

  if (digitalRead(pinSW[0]) == 1) {
    digitalWrite(pinLED[0], HIGH);
  }

  else if (digitalRead(pinSW[1]) == 1) {
    digitalWrite(pinLED[1], HIGH);
  }

  else if (digitalRead(pinSW[2]) == 1) {
    digitalWrite(pinLED[2], HIGH);
  }

  else if (digitalRead(pinSW[3]) == 1) {
    digitalWrite(pinLED[3], HIGH);
  }

  else {
    for (int k = 0; k < 4; k++) {
      digitalWrite(pinLED[k], LOW);
    }
  }
}  
```

```cpp
int leds[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13};
int numLeds = 13;

void setup() {
  for (int i = 0; i < numLeds; i++) {
    pinMode(leds[i], OUTPUT);
  }
}

void loop() {
  for (int i = 0; i < numLeds; i++) {
    digitalWrite(leds[i], HIGH);
    delay(300);
    digitalWrite(leds[i], LOW);
    delay(300);
  }
}
```
--- 

```cpp
int upSW = 26;
int downSW = 24;

void setup() {
  pinMode(upSW, INPUT);
  pinMode(downSW, INPUT);

  // LED 4~13
  for (int i = 4; i <= 13; i++) {
    pinMode(i, OUTPUT);
    digitalWrite(i, LOW);
  }
}

void loop() {

  // UP 버튼 → 13에서 4로
  if (digitalRead(upSW) == HIGH) {
    for (int i = 13; i >= 4; i--) {
      digitalWrite(i, HIGH);
      delay(200);
    }

    // 전부 끄기
    for (int i = 4; i <= 13; i++) {
      digitalWrite(i, LOW);
    }

    delay(300);
  }

  // DOWN 버튼 → 4에서 13으로
  if (digitalRead(downSW) == HIGH) {
    for (int i = 4; i <= 13; i++) {
      digitalWrite(i, HIGH);
      delay(200);
    }

    // 전부 끄기
    for (int i = 4; i <= 13; i++) {
      digitalWrite(i, LOW);
    }

    delay(300);
  }
}
```
---  

```cpp
int pinLED[4] = {4,5,6,7};
int k;

void setup() {
  for (k = 0; k < 4; k++) {
    pinMode(pinLED[k], OUTPUT);
  }
}

void loop() {
  LEDft1();
  LEDft2();
  LEDft3();
  LEDft4();
}

void LEDft1() {
  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], HIGH);
  }

  delay(1000);

  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], LOW);
  }

  delay(1000);
}

void LEDft2() {
  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], HIGH);
    delay(1000);
  }

  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], LOW);
    delay(1000);
  }
}

void LEDft3() {
  for (k = 3; k >= 0; k--) {
    digitalWrite(pinLED[k], HIGH);
    delay(1000);
  }

  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], LOW);
    delay(1000);
  }
}

void LEDft4() {
  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], HIGH);
    delay(1000);

    digitalWrite(pinLED[k], LOW);
    delay(1000);
  }
}
```
