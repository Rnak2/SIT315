#include <Wire.h>
#include <Adafruit_LiquidCrystal.h>


Adafruit_LiquidCrystal lcd(0);
const int trigPin = 9;
const int echoPin = 10;
const int interruptPin = 2; //button
volatile long duration; //volatile can be changed at anytime (shared between isr and main prog
volatile int distance;
volatile bool buttonPressed = false; 

void setup() {
  //start Serial Monitor
  Serial.begin(9600);
  Serial.println("Serial started");

  //start the LCD
  lcd.begin(16, 2);
  lcd.setBacklight(HIGH);
  lcd.setCursor(0, 0);

  //pins
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  //setup interrupt pin
  pinMode(interruptPin, INPUT_PULLUP); //set interupt pin to high by default and when button is pressed state low (easy to detect) 
  attachInterrupt(digitalPinToInterrupt(interruptPin), handleButtonPress, CHANGE);//interrupt will be triggered whenever the pin changes

  //print to LCD
  lcd.setCursor(0, 0);
  lcd.print("Distance:");
  Serial.println("LCD starts");
}

void loop() {
  //if button was pressed, measure distance
  if (buttonPressed) {
    buttonPressed = false; //reset to false

    measureDistance();
  }
}

void handleButtonPress() {
  static unsigned long lastInterruptTime = 0;
  unsigned long interruptTime = millis();

  if (interruptTime - lastInterruptTime > 200) {
    buttonPressed = true; //only true when > 200 to avoid bounce 
  }

  lastInterruptTime = interruptTime;
}

void measureDistance() {
  //operating distance sensor
  
  //clear previous signal
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  //initiate trig pin
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  //calculate distance using echo pin
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  //print in serial monitor 
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  //print to lcd
  lcd.setCursor(0, 1);
  lcd.print(distance);
  lcd.print(" cm  ");
}
