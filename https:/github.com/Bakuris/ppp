#include <Wire.h>
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27,16,2);

const int analogInPin = A0; 
int sensorValue = 0; 
unsigned long int avgValue; 
float b;
int buf[10],temp=0;



int encoderPinA = 8; // CLK pin
int encoderPinB = 9; // DT pin
int encoderBtn = 10; // SW pin
int encoderValue =  5.70;
int encoderValue2 = 6.00;
int encoderPinA_prev;
int encoderPinA_value;
boolean bool_CW;



void setup() 
{
  lcd.init();
  lcd.backlight();

  lcd.setCursor(0,0); // set cursor to 1 symbol of 1 line
  lcd.print("PH Controller");

  lcd.setCursor(0,1); // set cursor to 1 symbol of 2 line
  lcd.print("www.JUMANJI.ge"); 
    delay(2000);
     lcd.clear();
 Serial.begin(9600);
  pinMode (encoderPinA, INPUT);
  pinMode (encoderPinB, INPUT);
  pinMode(encoderBtn, INPUT_PULLUP);
  encoderPinA_prev = digitalRead(encoderPinA);
  pinMode(13,OUTPUT);
  
  lcd.begin(16, 2);

}
 
void loop() 
{
  encoderPinA_value = digitalRead(encoderPinA);
if (encoderPinA_value != encoderPinA_prev)
  {
    if (digitalRead(encoderPinB) != encoderPinA_value)
    {
      // if pin A state changed before pin B, rotation is clockwise
      
     
      encoderValue++;
       bool_CW = true;
    }
    else
    {
      // if pin B state changed before pin A, rotation is counter-clockwise
     
      bool_CW = false;
       encoderValue--;
    }

   if (bool_CW)
    {
      Serial.print("Clockwise | ");
    }
    else
    {
      Serial.print("Counter-Clockwise | ");
    }
    Serial.println(encoderValue);
  }
  encoderPinA_prev = encoderPinA_value;

  
  // check if button is pressed (pin SW)
  if (digitalRead(encoderBtn) == LOW)
  {
   Serial.println("Button Pressed");
  }
  else
  {
    Serial.println("Button Released");
  }
  
 for(int i=0;i<10;i++) 
 { 
  buf[i]=analogRead(analogInPin);
  delay(10);
 }
 for(int i=0;i<9;i++)
 {
  for(int j=i+1;j<10;j++)
  {
   if(buf[i]>buf[j])
   {
    temp=buf[i];
    buf[i]=buf[j];
    buf[j]=temp;
   }
  }
 }
 avgValue=0;
 for(int i=2;i<8;i++)
 avgValue+=buf[i];
 
 float pHVol=(float)avgValue*5.0/1024/4.3;
 float phValue = -5.70 * pHVol +29.5 ;
 phValue=14.2-phValue;
 //float phValue = -3.0 * pHVol+17.5;
 Serial.print("sensor = ");
 Serial.println(phValue);
 lcd.clear();
 lcd.setCursor(0,0);  
 lcd.print("PH");
 lcd.setCursor(0,1);  
 lcd.print(" ");
 lcd.setCursor(3,0);  
 lcd.print("Live");
 lcd.setCursor(3,1);  
 lcd.print(phValue);
 lcd.setCursor(8,0);  
 lcd.print("min");
 lcd.setCursor(8,1);  
 lcd.print("MAX");
 lcd.setCursor(12,0);  
 lcd.print(encoderValue);
 lcd.setCursor(12,1);  
 lcd.print(encoderValue2);
 delay(500);
}

int checkPH()
{
//if (encoderValue () < encoderValue)
  {
    digitalWrite(12,HIGH);
  }
 // else
  {
    digitalWrite(12,LOW);
  }
  //if (encoderValue () > encoderValue2)
  {
    digitalWrite(11,HIGH);
  }
 // else
  {
    digitalWrite(11,LOW);
  }
}
