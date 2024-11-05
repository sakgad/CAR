#include <IRremote.h>
int Dir1Pin_A = 1;
int Dir2Pin_A = 2;
int SpeedPin_A = 3;
int Dir1Pin_B = 4;
int Dir2Pin_B = 5;
int SpeedPin_B = 6;
int Dir1Pin_C = 7;
int Dir2Pin_C = 8;
int SpeedPin_C = 9;
int Dir1Pin_D = 11;
int Dir2Pin_D = 12;
int SpeedPin_D = 10;
 
int IRsensor = A0;
IRrecv irrecv(IRsensor);
decode_results results;

void setup() {
  pinMode(Dir1Pin_A, OUTPUT);
  pinMode(Dir2Pin_A, OUTPUT);
  pinMode(SpeedPin_A, OUTPUT);
  pinMode(Dir1Pin_B, OUTPUT);
  pinMode(Dir2Pin_B, OUTPUT);
  pinMode(SpeedPin_B, OUTPUT);
  pinMode(Dir1Pin_C, OUTPUT);
  pinMode(Dir2Pin_C, OUTPUT);
  pinMode(SpeedPin_C, OUTPUT);
  pinMode(Dir1Pin_D, OUTPUT);
  pinMode(Dir2Pin_D, OUTPUT);
  pinMode(SpeedPin_D, OUTPUT);
  Serial.begin(9600);
  irrecv.enableIRIn();
}

void loop() {
  if (irrecv.decode(&results)) {
    Serial.println(results.value, HEX);
    irrecv.resume();
    // digitalWrite(Dir1Pin_A, HIGH);
    // digitalWrite(Dir2Pin_A, LOW);
    // analogWrite(SpeedPin_A, 255);
    // digitalWrite(Dir1Pin_B, HIGH);
    // digitalWrite(Dir2Pin_B, LOW);
    // analogWrite(SpeedPin_B, 255);
    // digitalWrite(Dir1Pin_C, HIGH);
    // digitalWrite(Dir2Pin_C, LOW);
    // analogWrite(SpeedPin_C, 255);
    // digitalWrite(Dir1Pin_D, HIGH);
    // digitalWrite(Dir2Pin_D, LOW);
    // analogWrite(SpeedPin_D, 255);
  } 
  else {
    // digitalWrite(Dir1Pin_A, LOW);
    // digitalWrite(Dir2Pin_A, LOW);
    // analogWrite(SpeedPin_A, 0);
    // digitalWrite(Dir1Pin_A, LOW);
    // digitalWrite(Dir2Pin_A, LOW);
    // analogWrite(SpeedPin_A, 0);
    // digitalWrite(Dir1Pin_B, LOW);
    // digitalWrite(Dir2Pin_B, LOW);
    // analogWrite(SpeedPin_B, 0);
    // digitalWrite(Dir1Pin_C, LOW);
    // digitalWrite(Dir2Pin_C, LOW);
    // analogWrite(SpeedPin_C, 0);
    // digitalWrite(Dir1Pin_D, LOW);
    // digitalWrite(Dir2Pin_D, LOW);
    // analogWrite(SpeedPin_D, 0);
  }
}
