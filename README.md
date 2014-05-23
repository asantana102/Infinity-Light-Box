Infinity-Light-Box
==================
int receiverpin = 11;
int led = 3;  //B
int led2 = 5; //G
int led3 = 6; //R
int onOff=0;
int channel = 0;
int color = 50;
#include <IRremote.h>         
IRrecv irrecv(receiverpin); 
decode_results results;         

void setup(){
  Serial.begin(9600);
  irrecv.enableIRIn();
  pinMode(led,OUTPUT);
  pinMode(led2,OUTPUT);
  pinMode(led3,OUTPUT);
}

void loop(){
  if(irrecv.decode(&results)){
switch(results.value){
  
  case 0xA90:

  if(onOff==1){
    
    digitalWrite(led,LOW);
    
    digitalWrite(led2,LOW);
    
    digitalWrite(led3,LOW);
    
    onOff=0;
    
    delay(500);
  }
  
  else{
    
    digitalWrite(led,HIGH);
    
    digitalWrite(led2,HIGH);
    
    digitalWrite(led3,HIGH);
    
    onOff=1;
    
    delay(500);
  }
  break;
  case 0x290:
  if(channel==1){
  analogWrite(led,+color);
  analogWrite(led2,+color);
  analogWrite(led3,+color);
    channel=0;
    
    delay(1);
  }
  else{
    
  analogWrite(led,0-color);
  analogWrite(led2,0-color);
  analogWrite(led3,0-color);
    channel=1;
    
    delay(1);
  }
  break; 
case 0x010:
  case 0x810:
analogWrite(led,255);
  analogWrite(led2,0);
  analogWrite(led3,0);
  break;
case 0x410:
analogWrite(led,0);
  analogWrite(led2,0);
  analogWrite(led3,255);
  break;
case 0xC10:
  analogWrite(led,255);
  analogWrite(led2,128);
  analogWrite(led3,0);
  break;
case 0x210:
  analogWrite(led,255);
  analogWrite(led2,0);
  analogWrite(led3,255);
  break;
case 0xA10:
  analogWrite(led,255);
  analogWrite(led2,51);
  analogWrite(led3,255);
  break;
case 0x610:
  analogWrite(led,255);
  analogWrite(led2,69);
  analogWrite(led3,0);
  break;
case 0xE10:
  analogWrite(led,210);
  analogWrite(led2,105);
  analogWrite(led3,30);
  break;
case 0x110:
  analogWrite(led,250);
  analogWrite(led2,240);
  analogWrite(led3,230);
  break;
case 0x910:
  analogWrite(led,255);
  analogWrite(led2,20);
  analogWrite(led3,147);
  break;
}
   if (irrecv.decode(&results)){
Serial.print(results.value,HEX);
Serial.print(" ");
irrecv.resume();
  
}
  }
}
