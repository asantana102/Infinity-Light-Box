Infinity-Light-Box
==================
int receiverpin = 3;
int blue = 11;
int green = 10;
int red = 9;
int onOff=0;
int channel = 0;
int color = 50;
#include <IRremote.h>         
IRrecv irrecv(receiverpin); 
decode_results results;    

void setup()
{
  Serial.begin(9600);
  irrecv.enableIRIn();
  pinMode(green, OUTPUT);
  pinMode(blue, OUTPUT);
  pinMode(red, OUTPUT);
}

void loop()
{
  if(irrecv.decode(&results)){
switch(results.value){
  
  
  
  case 0xA90:

  if(onOff==1){
    
    digitalWrite(green,LOW);
    digitalWrite(blue,LOW);
    digitalWrite(red,LOW);
    
    onOff=0;
    
    delay(500);
  }
  
  else{
    
    digitalWrite(green,HIGH);
    
    digitalWrite(blue,HIGH);
    
    digitalWrite(red,HIGH);
    
    onOff=1;
    
    delay(500);
  }
  break;
  
  case 0x290:
  if(channel==1){
  analogWrite(green,+color);
  analogWrite(blue,+color);
  analogWrite(red,+color);
    channel=0;
    
    delay(1);
  }
  else{
    
  analogWrite(green,0-color);
  analogWrite(blue,0-color);
  analogWrite(red,0-color);
    channel=1;
    
    delay(1);
  }
  break;
  
case 0x010:
  case 0x810:
  analogWrite(green,255);
  analogWrite(blue,0);
  analogWrite(red,0);
  break;

case 0x410:
  analogWrite(green,0);
  analogWrite(blue,0);
  analogWrite(red,255);
  break;
  
case 0xC10:
  analogWrite(green,255);
  analogWrite(blue,128);
  analogWrite(red,0);
  break;
case 0x210:
  analogWrite(green,255);
  analogWrite(blue,0);
  analogWrite(red,255);
  break;
case 0xA10:
  analogWrite(green,255);
  analogWrite(blue,51);
  analogWrite(red,255);
  break;
case 0x610:
  analogWrite(green,255);
  analogWrite(blue,69);
  analogWrite(red,0);
  break;
case 0xE10:
  analogWrite(green,210);
  analogWrite(blue,105);
  analogWrite(red,30);
  break;
case 0x110:
  analogWrite(green,250);
  analogWrite(blue,240);
  analogWrite(red,230);
  break;
case 0x910:
  analogWrite(green,255);
  analogWrite(blue,20);
  analogWrite(red,147);
  break;
}
   if (irrecv.decode(&results)){
Serial.print(results.value,HEX);
Serial.print(" ");
irrecv.resume();

  
}
  }
}
