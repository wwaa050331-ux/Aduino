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
---  

# Final Exam  
### week9  
---    
#### 부저를 이용해 도레미파솔라시 음계를 자동으로 반복해서 재생하는 코드

- pinMode(50, OUTPUT) : 50번 핀을 출력 모드로 설정해.
  
- tone(50, 262, 100) : 50번 핀에서 도 음을 100ms 동안 재생해.
  
- delay(500) : 500ms 동안 기다려.

- loop() : 도부터 시까지 재생하는 동작을 계속 반복해.

---  

```cpp
void setup() {
  pinMode(50, OUTPUT);  // 부저 핀 설정
}

void loop() {
  tone(50, 262, 100);  // 도
  delay(500);

  tone(50, 294, 100);  // 레
  delay(500);

  tone(50, 330, 100);  // 미
  delay(500);

  tone(50, 349, 100);  // 파
  delay(500);

  tone(50, 392, 100);  // 솔
  delay(500);

  tone(50, 440, 100);  // 라
  delay(500);

  tone(50, 494, 100);  // 시
  delay(500);
}
```
---   
# week10   

##  ① 커서 깜박이기 → ② 숫자 0~10 카운트업 → ③ Hello! 3번 깜박이기  

---  

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  lcd.init();
  lcd.backlight();

  // =================================
  // 1. Cursor ON-Blink / OFF
  // =================================

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Cursor ON-Blink");

  lcd.setCursor(0, 1);
  lcd.cursor();
  lcd.blink();

  delay(2000);  // 2초 깜박임

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Cursor OFF");

  lcd.setCursor(0, 1);
  lcd.cursor();
  lcd.blink();

  delay(1000);

  lcd.noBlink();  // 깜박임 정지

  delay(1000);

  lcd.noCursor(); // 커서 제거

  delay(1000);

  lcd.clear();


  // =================================
  // 2. Count up (0 ~ 10)
  // =================================

  lcd.setCursor(0, 0);
  lcd.print("Count up");

  delay(1000);

  for (int k = 0; k <= 10; k++) {
    lcd.setCursor(0, 0);
    lcd.print("No : ");
    lcd.print(k);
    lcd.print("  ");

    delay(200);  // 0.2초 간격
  }

  lcd.clear();


  // =================================
  // 3. Hello! 3번 깜박이기
  // =================================

  lcd.setCursor(0, 0);
  lcd.print("Hello!");

  for (int k = 0; k < 3; k++) {
    lcd.noDisplay();  // 화면 끄기
    delay(1000);

    lcd.display();    // 화면 켜기
    delay(1000);
  }

  lcd.clear();
```

```cpp

#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  lcd.init();
  lcd.backlight();

  // =================================
  // 1. Cursor ON-Blink / OFF
  // =================================

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Cursor ON-Blink");

  lcd.setCursor(0, 1);
  lcd.cursor();
  lcd.blink();

  delay(2000);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Cursor OFF");

  lcd.setCursor(0, 1);
  lcd.cursor();
  lcd.blink();

  delay(1000);

  lcd.noBlink();
  delay(1000);

  lcd.noCursor();
  delay(1000);

  lcd.clear();


  // =================================
  // 2. Count up (0 ~ 10)
  // =================================

  lcd.setCursor(0, 0);
  lcd.print("Count up");

  delay(1000);

  for (int k = 0; k <= 10; k++) {
    lcd.setCursor(0, 0);
    lcd.print("No : ");
    lcd.print(k);
    lcd.print("  ");

    delay(200);
  }

  lcd.clear();


  // =================================
  // 3. Hello! 3번 깜박이기
  // =================================

  lcd.setCursor(0, 0);
  lcd.print("Hello!");

  for (int k = 0; k < 3; k++) {
    lcd.noDisplay();
    delay(1000);

    lcd.display();
    delay(1000);
  }

  lcd.clear();


  // =================================
  // 4. Hello 오른쪽 / 왼쪽 이동
  // =================================

  lcd.setCursor(6, 0);
  lcd.print("Hello");

  // 오른쪽으로 3번 이동
  for (int k = 0; k < 3; k++) {
    lcd.scrollDisplayRight();
    delay(1000);
  }

  // 왼쪽으로 3번 이동
  for (int k = 0; k < 3; k++) {
    lcd.scrollDisplayLeft();
    delay(1000);
  }

  lcd.clear();
}

void loop() {
}


---


}

void loop() {
}
```  

---  
# week12  

### 초음파 센서(TRIG 37, ECHO 41)로 물체까지의 왕복 시간을 측정해 cm와 inch 단위로 동시에 거리를 계산합니다.

### PUSH_UP(26번) 버튼을 누르면 LCD 화면에 센티미터(cm) 단위로, PUSH_DOWN(24번) 버튼을 누르면 인치(inch) 단위로 거리를 출력합니다.

### 측정 범위를 벗어나면(400cm / 157inch 초과 또는 0) Out of Range를 표시하며, 현재 올려주신 텍스트는 동일한 코드가 두 번 중복되어 있으니 한 번만 남기고 사용하셔야 합니다.  

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

#define PUSH_UP 26
#define PUSH_DOWN 24
#define TRIG 37 // 트리거 핀을 지정
#define ECHO 41 // 에코 핀을 지정

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup()
{
  lcd.init();
  lcd.backlight();
  lcd.clear();
  
  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);
  pinMode(PUSH_UP, INPUT);
  pinMode(PUSH_DOWN, INPUT);
}

void loop()
{
  // 1. 초음파 펄스 발생 (10us 이상 유지)
  digitalWrite(TRIG, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG, LOW);

  // 2. 에코 신호 수신 (30ms 타임아웃 설정으로 무한 대기 방지)
  long Time = pulseIn(ECHO, HIGH, 30000);
  long distance_cm = Time / 58;
  long distance_inch = Time / 148;

  // 3. PUSH_UP 버튼 눌렀을 때 (cm 출력)
  if (digitalRead(PUSH_UP) == HIGH)
  {
    lcd.setCursor(0, 0);
    lcd.print("DIST:  ");
    lcd.setCursor(7, 0);
    
    // 측정 범위를 벗어나거나(400cm 초과) 수신 실패(0)일 때 예외 처리
    if (distance_cm == 0 || distance_cm > 400) {
      lcd.print("Out of Range");
    } else {
      lcd.print(String(distance_cm) + " cm     "); // 뒤 공백으로 잔상 제거
    }
  }

  // 4. PUSH_DOWN 버튼 눌렀을 때 (inch 출력)
  if (digitalRead(PUSH_DOWN) == HIGH)
  {
    lcd.setCursor(0, 0);
    lcd.print("DIST:  ");
    lcd.setCursor(7, 0);
    
    if (distance_inch == 0 || distance_inch > 157) {
      lcd.print("Out of Range");
    } else {
      lcd.print(String(distance_inch) + " inch   "); // 뒤 공백으로 잔상 제거
    }
  }

  delay(100);
}

```

### 초음파 센서(TRIG 37, ECHO 41)로 물체까지의 거리를 측정하여 cm 단위로 실시간 계산합니다.

### 측정 거리가 25cm 이하일 때는 경고 구간으로 판단해 LCD에 Warning을 띄우고 경고 LED를 점등하며, 400cm를 초과하면 Out of range를 표시합니다.

### 정상 및 경고 구간 모두 LCD와 4자리 FND(7세그먼트)에 현재 거리를 동시에 출력합니다.  
```cpp  
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <TM1637Display.h> // 4자리 FND(7세그먼트) 라이브러리

// 1. 핀 번호 설정 (첫 번째 사진 및 보드 기준)
#define TRIG 37
#define ECHO 41

// ★ 보드에 연결된 FND(CLK, DIO) 및 LED 핀 번호로 수정하세요!
#define FND_CLK 2
#define FND_DIO 3
#define LED_PIN 13  // 경고 LED 핀 (여러 개라면 배열로 확장 가능)

LiquidCrystal_I2C lcd(0x27, 16, 2);
TM1637Display display(FND_CLK, FND_DIO);

void setup() {
  Serial.begin(9600);
  
  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);
  pinMode(LED_PIN, OUTPUT);

  // LCD 초기화
  lcd.init();
  lcd.backlight();
  lcd.clear();

  // FND(7세그먼트) 밝기 설정 (0~7)
  display.setBrightness(0x0f);
}

void loop() {
  // 초음파 발사
  digitalWrite(TRIG, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG, LOW);

  // 거리 계산 (cm)
  long duration = pulseIn(ECHO, HIGH);
  long distance = duration / 58.2;

  lcd.clear();

  // 1. 범위 초과 (Out of range: 0 이하이거나 400cm 초과)
  if (distance <= 0 || distance > 400) {
    lcd.setCursor(0, 0);
    lcd.print("Distance System");
    lcd.setCursor(0, 1);
    lcd.print("Out of range");
    
    display.clear(); // FND 끄기
    digitalWrite(LED_PIN, LOW);
  }
  // 2. 경고 구간 (영상 기준 25cm 이하일 때 Warning 표시 및 LED 점등)
  else if (distance <= 25) {
    lcd.setCursor(0, 0);
    lcd.print("Warning");
    lcd.setCursor(0, 1);
    lcd.print("Distance: ");
    lcd.print(distance);
    lcd.print(" cm");

    display.showNumberDec(distance, false); // FND에 거리 출력
    digitalWrite(LED_PIN, HIGH);            // LED 켜기
  }
  // 3. 정상 구간 (25cm 초과 ~ 400cm 이하)
  else {
    lcd.setCursor(0, 0);
    lcd.print("Distance System");
    lcd.setCursor(0, 1);
    lcd.print("Distance: ");
    lcd.print(distance);
    lcd.print(" cm");

    display.showNumberDec(distance, false); // FND에 거리 출력
    digitalWrite(LED_PIN, LOW);             // LED 끄기
  }

  delay(200); // 화면 깜빡임 방지를 위한 딜레이
}  


```

