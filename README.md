#IOT
Here I have Used Arduino Uno and other componets which works on the principle of Mutual Induction.
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,16,2);

#define IR_SENSOR 8
#define RELAY 10

void setup()
{
  pinMode(IR_SENSOR, INPUT);
  pinMode(RELAY, OUTPUT);

  digitalWrite(RELAY, LOW);

  lcd.init();
  lcd.backlight();

  lcd.setCursor(0,0);
  lcd.print("Wireless EV");
  lcd.setCursor(0,1);
  lcd.print("Charging Sys");

  delay(2000);
  lcd.clear();
}

void loop()
{
  int state = digitalRead(IR_SENSOR);

  if(state == LOW)
  {
      digitalWrite(RELAY,HIGH);

      lcd.setCursor(0,0);
      lcd.print("Vehicle Found ");

      lcd.setCursor(0,1);
      lcd.print("Charging ON   ");
  }
  else
  {
      digitalWrite(RELAY,LOW);

      lcd.setCursor(0,0);
      lcd.print("Waiting...    ");

      lcd.setCursor(0,1);
      lcd.print("Charging OFF  ");
  }

  delay(100);
}
