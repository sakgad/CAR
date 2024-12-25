### 자동차 코드

```
#include <IRremote.hpp>  // IRremote 라이브러리 포함

#define IR_RECEIVE_PIN 3  // 수신기 핀 번호 (D3 핀 등 사용 가능)

int Dir1Pin_A = 2;      // 제어신호 1핀
int Dir2Pin_A = 4;      // 제어신호 2핀
int SpeedPin = 5;
int Dir1Pin_B = 6;
int Dir2Pin_B = 7;
int Dir1Pin_C = 8;
int Dir2Pin_C = 9;
int Dir1Pin_D = 10;
int Dir2Pin_D = 11;
int go = 0;
int dir = 0;

void setup() {
    Serial.begin(115200);
    pinMode(LED_BUILTIN, OUTPUT);  // 내장 LED 핀을 출력으로 설정

    // IR 수신기 초기화
    IrReceiver.begin(IR_RECEIVE_PIN, ENABLE_LED_FEEDBACK);  // 수신 핀 번호와 LED 피드백 활성화
    Serial.println("IR 수신 대기 중...");

    pinMode(SpeedPin, OUTPUT);
    pinMode(Dir1Pin_A, OUTPUT);
    pinMode(Dir2Pin_A, OUTPUT);
    pinMode(Dir1Pin_B, OUTPUT);
    pinMode(Dir2Pin_B, OUTPUT);
    pinMode(Dir1Pin_C, OUTPUT);
    pinMode(Dir2Pin_C, OUTPUT);
    pinMode(Dir1Pin_D, OUTPUT);
    pinMode(Dir2Pin_D, OUTPUT);
}

void loop() {
    // IR 수신 대기
    if (IrReceiver.decode()) {  
        // 신호를 수신한 경우
        Serial.print("Received IR signal: ");
        
        // 수신된 신호 정보 출력 (주소 및 명령)
        Serial.print("Address: 0x");
        Serial.print(IrReceiver.decodedIRData.address, HEX);  // 수신된 주소 출력
        Serial.print(", Command: 0x");
        Serial.println(IrReceiver.decodedIRData.command, HEX);  // 수신된 명령 출력

        // 특정 명령을 수신했을 때 "hi" 출력
        if (IrReceiver.decodedIRData.command == 0x32) {  // 예: 0x34 명령 수신
          go = 1;
          dir = -1;
        }
        else if (IrReceiver.decodedIRData.command == 0x33) {
          go = 1;
          dir = 1;
        }
        else if (IrReceiver.decodedIRData.command == 0x34) {
          go = 1;
          dir = 0;
        }
        else if (IrReceiver.decodedIRData.command == 0x35) {
          go = 0;
          dir = 0;
        }
        else if (IrReceiver.decodedIRData.command == 0x36) {
          go = -1;
          dir = -1;
        }
        else if (IrReceiver.decodedIRData.command == 0x37) {
          go = -1;
          dir = 1;
        }
        else if (IrReceiver.decodedIRData.command == 0x38) {
          go = -1;
          dir = 0;
        }
        // 내장 LED를 깜빡여서 수신 확인
        digitalWrite(LED_BUILTIN, HIGH);  // LED 켜기
        delay(100);  // 100ms 대기
        digitalWrite(LED_BUILTIN, LOW);  // LED 끄기

        // 수신된 데이터 초기화
        IrReceiver.resume();  // 수신기 상태 초기화
    }
    
    if (go == 1) {
      if (dir == -1) {
        digitalWrite(Dir1Pin_A, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_A, HIGH);
        digitalWrite(Dir1Pin_B, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_B, LOW);
        digitalWrite(Dir1Pin_C, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_C, LOW);
        digitalWrite(Dir1Pin_D, HIGH);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_D, LOW);
      }
      else if (dir == 1) {
        digitalWrite(Dir1Pin_A, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_A, LOW);
        digitalWrite(Dir1Pin_B, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_B, HIGH);
        digitalWrite(Dir1Pin_C, HIGH);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_C, LOW);
        digitalWrite(Dir1Pin_D, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_D, LOW);
      }
      else if (dir == 0) {
        digitalWrite(Dir1Pin_A, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_A, HIGH);
        digitalWrite(Dir1Pin_B, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_B, HIGH);
        digitalWrite(Dir1Pin_C, HIGH);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_C, LOW);
        digitalWrite(Dir1Pin_D, HIGH);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_D, LOW);
      }
      analogWrite(SpeedPin, 255);          //모터 속도를 최대로 설정
    } else if (go == -1) {
      if (dir == -1) {
        digitalWrite(Dir1Pin_A, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_A, LOW);
        digitalWrite(Dir1Pin_B, HIGH);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_B, LOW);
        digitalWrite(Dir1Pin_C, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_C, HIGH);
        digitalWrite(Dir1Pin_D, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_D, LOW);
      }
        if (dir == 1) {
        digitalWrite(Dir1Pin_A, HIGH);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_A, LOW);
        digitalWrite(Dir1Pin_B, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_B, LOW);
        digitalWrite(Dir1Pin_C, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_C, LOW);
        digitalWrite(Dir1Pin_D, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_D, HIGH);
      }
        if (dir == 0) {
        digitalWrite(Dir1Pin_A, HIGH);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_A, LOW);
        digitalWrite(Dir1Pin_B, HIGH);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_B, LOW);
        digitalWrite(Dir1Pin_C, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_C, HIGH);
        digitalWrite(Dir1Pin_D, LOW);         //모터가 시계 방향으로 회전
        digitalWrite(Dir2Pin_D, HIGH);
      }
      analogWrite(SpeedPin, 255);          //모터 속도를 최대로 설정
    } else {
      digitalWrite(Dir1Pin_A, LOW);
      digitalWrite(Dir2Pin_A, LOW);
      digitalWrite(Dir1Pin_B, LOW);
      digitalWrite(Dir2Pin_B, LOW);
      digitalWrite(Dir1Pin_C, LOW);
      digitalWrite(Dir2Pin_C, LOW);
      digitalWrite(Dir1Pin_D, LOW);
      digitalWrite(Dir2Pin_D, LOW);
    }
}
```

### 컨트롤러 코드

```
#include <IRremote.hpp>  // IRremote 라이브러리 포함

#define IR_SEND_PIN 6     // KY-005의 Signal 핀을 연결한 디지털 핀
const int buttonPin2 = 2;
const int buttonPin3 = 3;
const int buttonPin4 = 4;

void setup() {
    Serial.begin(115200);  // 시리얼 통신 시작
    pinMode(LED_BUILTIN, OUTPUT);  // 내장 LED 설정

    pinMode(buttonPin2, INPUT_PULLUP);  // 버튼 핀을 입력 모드로 설정 (풀업 저항 사용)
    pinMode(buttonPin3, INPUT_PULLUP);
    pinMode(buttonPin4, INPUT_PULLUP);

    // 송신기 초기화
    IrSender.begin(IR_SEND_PIN);  // IR 송신 핀 초기화
    Serial.println("조이스틱 버튼 확인 중...");
}

void loop() {
    int buttonPin2 = digitalRead(2);  // 버튼 상태 읽기 
    int buttonPin3 = digitalRead(3);
    int buttonPin4 = digitalRead(4);

    int x = analogRead(0);

    if (buttonPin4 == LOW) {  // 버튼이 눌리면 (LOW는 풀업 저항 사용 시 눌렸을 때)
        if (x > 540) {
          IrSender.sendNEC(0x00, 0x32, 0);
        }
        else if (x < 520) {
          IrSender.sendNEC(0x00, 0x33, 0);
        }
        else {
          IrSender.sendNEC(0x00, 0x34, 0);
        }
        digitalWrite(LED_BUILTIN, HIGH);  // LED 켜기 (버튼이 눌리면)
        delay(100);  // 잠시 대기
        digitalWrite(LED_BUILTIN, LOW);  // LED 끄기
    } else if (buttonPin3 == LOW) {
        IrSender.sendNEC(0x00, 0x35, 0);
        Serial.println("NEC 신호 송신: 주소=0x00, 명령=0x35");

        digitalWrite(LED_BUILTIN, HIGH);  // LED 켜기 (버튼이 눌리면)
        delay(100);  // 잠시 대기
        digitalWrite(LED_BUILTIN, LOW);  // LED 끄기
    } else if (buttonPin2 == LOW) {
        if (x > 540) {
          
          IrSender.sendNEC(0x00, 0x36, 0);
          Serial.print("hi");
        }
        else if (x < 520) {
          IrSender.sendNEC(0x00, 0x37, 0);
        }
        else {
          IrSender.sendNEC(0x00, 0x38, 0);
        }
        digitalWrite(LED_BUILTIN, HIGH);  // LED 켜기 (버튼이 눌리면)
        delay(100);  // 잠시 대기
        digitalWrite(LED_BUILTIN, LOW);  // LED 끄기
    } else {
        // 버튼이 눌리지 않으면 아무 것도 하지 않음
        digitalWrite(LED_BUILTIN, LOW);  // LED 끄기
    }

    delay(100);  // 100ms 대기
}
```
