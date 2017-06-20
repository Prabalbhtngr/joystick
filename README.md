 joystick
code for joystick

#include<SPI.h>
#inlude "nRF24L01.h"
#include "RF24.h"

#define cepin 9
#define csnpin 10
#define Xpin   A0
#definr Ypin A1

const byte rightpin = 3;
const byte uppin    = 2;
const byte downpin  = 4;
const byte leftpin  = 5;

const uint64_t pipe = 0xE1E2E3E4E5LL;

RF radio(cepin,csnpin);

int joustick[6];

void setup()
  { 
     Serial.begin(115200);
     radio.begin();
     radio.openWritingPipe(pipe);

     pinmMode(rightpin,INPUT);
     digitalWrite(rightpin,HIGH);

     pinmMode(leftpin,INPUT);
     digitalWrite(lefttpin,HIGH);

     pinmMode(uppin,INPUT);
     digitalWrite(uppin,HIGH);

     pinmMode(downpin,INPUT);
     digitalWrite(downpin,HIGH);

     
  }


void loop()
  {
     joystick[0]= analogRead(Xpin);
     joystick[1]= analogRead(Ypin);

     joystick[2]= digitalRead(uppin);
     joystick[3]= digitalRead(rightpin);
     joystick[4]= digitalRead(downpin);
     joystick[5]= digitalRead(leftpin);

     radio.Write(joystick,sizeof(joystick));
     

  }
