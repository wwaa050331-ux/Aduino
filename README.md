# Aduino 

## week2 스위치 순차적으로 켜기
---   
```cpp
// 핀 번호 설정
const int startPin = 2;
const int endPin = 11;
const int totalPins = (endPin - startPin) + 1; // 총 10개 (2~11번)

void setup() {
  // 2번부터 11번 핀까지 모두 출력(OUTPUT) 모드로 설정
  for (int i = startPin; i <= endPin; i++) {
    pinMode(i, OUTPUT);
    digitalWrite(i, LOW); // 시작할 때는 모두 끔
  }
}

void loop() {
  // 1번부터 10번까지 아래에서 위로 순서대로 켜기
  for (int i = startPin; i <= endPin; i++) {
    digitalWrite(i, HIGH); // 켜기
    delay(300);            // 0.3초 대기 (속도 조절 가능)
  }  
```
---

## week3 짝수번호만 LED 켜기

```cpp
// 핀 번호 설정
const int startPin = 2;
const int endPin = 11;

void setup() {
  // 2번부터 11번 핀까지 모두 출력(OUTPUT) 모드로 설정
  for (int i = startPin; i <= endPin; i++) {
    pinMode(i, OUTPUT);
    digitalWrite(i, LOW); // 시작할 때는 모두 끔
  }
}

void loop() {
  // 1. 짝수 핀만 순서대로 켜기 (2, 4, 6, 8, 10번)
  for (int i = startPin; i <= endPin; i++) {
    if (i % 2 == 0) {       // 핀 번호가 짝수일 때만 실행
      digitalWrite(i, HIGH); // 켜기
      delay(300);            // 0.3초 대기
    }
  }
```
---  

## week4 LCD화면 활용하기 

```cpp

#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// I2C LCD 주소 설정 (일반적으로 0x27 또는 0x3F를 사용합니다)
// LCD 크기: 16열 2행 (1602)
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  // LCD 초기화
  lcd.init();                      
  // 백라이트 켜기
  lcd.backlight();
}

void loop() {
  // 1. 커서 관련 메시지 출력 예시 (영상 초반)
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Curser Off");
  delay(2000);

  // 2. 카운트업 기능 예시 (영상 중반)
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Count Up");
  delay(1000);

  // 숫자가 1부터 5까지 증가하는 예시
  for (int i = 1; i <= 5; i += 2) {
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("No : ");
    lcd.print(i);
    delay(1000);
  }

  // 3. Hello! 문자열 출력 예시 (영상 후반)
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Hello!");
  delay(2000);

  // 두 번째 줄에도 출력하는 예시
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Hello!");
  lcd.setCursor(0, 1);
  lcd.print("Hello!");
  delay(3000);
}  
```
---

## week5    
## (1)
```cpp
// 4개의 LED가 연결된 디지털 핀 번호를 배열로 선언합니다 (4, 5, 6, 7번 핀)
int pinLED[4] = {4, 5, 6, 7};
int k; // 반복문에 사용할 변수 선언

void setup() {
  // 4개의 LED 핀을 모두 출력(OUTPUT) 모드로 설정합니다.
  for (k = 0; k < 4; k++) {
    pinMode(pinLED[k], OUTPUT);
  }
}

void loop() {
  // 정의된 4가지 LED 패턴 함수를 순서대로 무한 반복합니다.
  LEDft1();
  LEDft2();
  LEDft3();
  LEDft4();
}

// 1. 모든 LED를 동시에 켜고 끄는 함수
void LEDft1() {
  // 모든 LED 켜기
  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], HIGH);
  }
  delay(1000); // 1초 대기

  // 모든 LED 끄기
  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], LOW);
  }
  delay(1000); // 1초 대기
}

// 2. 순서대로(정방향) 하나씩 켜고, 순서대로 끄는 함수
void LEDft2() {
  // 4번 핀부터 7번 핀까지 1초 간격으로 차례대로 켜기
  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], HIGH);
    delay(1000);
  }

  // 4번 핀부터 7번 핀까지 1초 간격으로 차례대로 끄기
  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], LOW);
    delay(1000);
  }
}

// 3. 역순(거꾸로)으로 하나씩 켜고, 순서대로 끄는 함수
void LEDft3() {
  // 7번 핀부터 4번 핀까지 역순으로 1초 간격으로 켜기
  for (k = 3; k >= 0; k--) {
    digitalWrite(pinLED[k], HIGH);
    delay(1000);
  }

  // 4번 핀부터 7번 핀까지 순서대로 1초 간격으로 끄기
  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], LOW);
    delay(1000);
  }
}

// 4. 각 LED를 하나씩 켠 직후에 바로 끄는 것을 반복하는 함수
void LEDft4() {
  // 4번부터 7번 LED까지 각각 켜졌다가 바로 꺼지는 동작을 순차적으로 수행
  for (k = 0; k < 4; k++) {
    digitalWrite(pinLED[k], HIGH); // 켜기
    delay(1000);                  // 1초 대기

    digitalWrite(pinLED[k], LOW);  // 끄기
    delay(1000);                  // 1초 대기
  }
}  
```
---  
## (2)  실습3 - pwm led 밝기 제어   

```cpp

#define DELAY_TIME 300

int pinPWM = 5;
int k;

void setup() {

  pinMode(pinPWM , OUTPUT);
}

void loop() {
  
  for(k=0 ; k<=255;k++){
    analogWrite(pinPWM,k);
    delay(15);
  }
  for(k=255 ; k>=0;k--){
    analogWrite(pinPWM,k);
    delay(15);
  }
}
```

---     

## week6 up sw,down sw 켰다 껐다
(1)  
```cpp
int upSW = 26;
int downSW = 24;

int ledUp = 4;
int ledDown = 13;

int upState = LOW;
int downState = LOW;

void setup() {
  pinMode(upSW, INPUT);
  pinMode(downSW, INPUT);

  pinMode(ledUp, OUTPUT);
  pinMode(ledDown, OUTPUT);

  digitalWrite(ledUp, LOW);
  digitalWrite(ledDown, HIGH);
}

void loop() {

  // UP 스위치를 누르면 LED 4번 ON/OFF
  if (digitalRead(upSW) == HIGH) {
    upState = !upState;
    digitalWrite(ledUp, upState);
    delay(200);
  }

  // DOWN 스위치를 누르면 LED 13번 ON/OFF
  if (digitalRead(downSW) == HIGH) {
    downState = !downState;
    digitalWrite(ledDown, downState);
    delay(200);
  }
}  
```

---
## up sw,down sw 내리기 올리기
(2)

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

## week7 LCD의 밝기 측정  

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// I2C LCD 주소 설정 (일반적으로 0x27 또는 0x3F)
// 16열 2행 LCD 설정
LiquidCrystal_I2C lcd(0x27, 16, 2);

int cdsPin = A0; // 조도 센서가 연결된 아날로그 핀

void setup() {
  // LCD 초기화 및 백라이트 켜기
  lcd.init();
  lcd.backlight();
}

void loop() {
  // 1. 조도 센서 값 읽기 (0 ~ 1023 또는 변환된 값)
  int cdsValue = analogRead(cdsPin);

  // 2. 첫 번째 줄(0번째 열, 0번째 행)에 이름 출력
  lcd.setCursor(0, 0);
  lcd.print("An Yuri");  // 원하시는 이름으로 변경 가능합니다.

  // 3. 두 번째 줄(0번째 열, 1번째 행)에 조도 센서 값 출력
  lcd.setCursor(0, 1);
  lcd.print("lux= ");
  lcd.print(cdsValue);
  
  // 숫자가 바뀔 때 잔상이 남지 않도록 빈 칸 채우기(선택사항)
  lcd.print("   "); 

  delay(500); // 0.5초마다 갱신
}
```
