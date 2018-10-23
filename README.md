
#include <SPI.h>
#include <MFRC522.h>
#include <SoftwareSerial.h>


#define RST_PIN         11       
#define SS_PIN          10  

String cardno,cardnotemp;
MFRC522 mfrc522(SS_PIN, RST_PIN); 
String web;

int counter=0;





void setup()
{
  Serial.begin(115200);
   SPI.begin();

  pinMode(A0,INPUT);
  pinMode(11,OUTPUT);

  sensor();
  
}


void dump_byte_array(byte *buffer, byte bufferSize)
{
    for (byte i = 0; i < bufferSize; i++) 
    {
        cardno.concat(String(buffer[i],HEX));
    }
}


void loop()
{
  cardno="";

   dump_byte_array(mfrc522.uid.uidByte, mfrc522.uid.size);
 // sensor();



   /*
   if (analogRead(A0)<50)
  {
     digitalWrite(11,HIGH);
    if(counter==0)
    {
     Serial.print("  bicycle detected   ");
     counter=1;
    }
  }

  else
     {
    
     digitalWrite(11,LOW);
    if(counter==1)
    {
     Serial.print("   bicycle not detected  ");
     counter=0;
    }
    
     }
 delay (100);
 */ 
}


void sensor()
{
  
  Serial.print("bicycle_start");
  
  
  
  while(true)
  {
    
  if (analogRead(A0)<50)
  {
     digitalWrite(11,HIGH);
   if(counter==0)
    {
     Serial.print("bicycle_detected");
     counter=1;
    }
  }

  else
     {
    
     digitalWrite(11,LOW);
    if(counter==1)
    {
     Serial.print("bicycle_not_detected");
     counter=0;
    }
    
     }
     
   delay (10);
    }
     
}
