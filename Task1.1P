#include <Wire.h>
#include <Adafruit_LiquidCrystal.h>

// Initialize the LCD with the I2C address (commonly 0x27 or 0x3F)
Adafruit_LiquidCrystal lcd(0);

const int trigPin = 9;
const int echoPin = 10;
long duration;
int distance;

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
  
  //print to LCD
  lcd.setCursor(0, 0);
  lcd.print("Distance:");
  Serial.println("LCD starts");
}

void loop() {
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
  
  delay(500);
}
