Underwater sensor node arduino code for all sensors and contacting with nodemcu


main code:

#include <OneWire.h>
#include <DallasTemperature.h>

// Data wire is conntect to the Arduino digital pin 4
#define ONE_WIRE_BUS 4
 
// Setup a oneWire instance to communicate with any OneWire devices
OneWire oneWire(ONE_WIRE_BUS);

// Pass our oneWire reference to Dallas Temperature sensor 
DallasTemperature sensors(&oneWire);


float sen1=0;
float sen2=0;
int sen3=0;

//pH sensor Variables:
int temp;
float sti;
int buf[10];
unsigned long int avgValue;

float calibration =30.043;// change c,it has to be changed for calibrating pH meter  


int pirSensor = 10;




//Temperature measurement:
float wtemp()
{
  sensors.requestTemperatures(); 
  sti=sensors.getTempCByIndex(0);
  return sti;
}


//pH measurement:
float phm() 
{
 for(int i=0;i<10;i++) 
 { 
 buf[i]=analogRead(0);
 delay(10);
 }
 for(int i=0;i<9;i++)
 {
 for(int j=i+1;j<10;j++)
 {
 if(buf[i]>buf[j])
 {
 float temp=buf[i];
 buf[i]=buf[j];
 buf[j]=temp;
 }
 }
 }
 avgValue=0;
 for(int i=2;i<8;i++)
 avgValue+=buf[i];
 float pHVol=(float)avgValue*5.0/1024/6;
 float phi = (-5.36 * pHVol)+ calibration;//y=mx+c,change m
 Serial.print("pH_voltage:");
 Serial.println(pHVol);
 return phi;
}
  

void setup() 
{ 
  Serial.begin(9600);
  Serial3.begin(9600);
  pinMode(pirSensor, INPUT);
  sensors.begin();
}


void loop() 
{     
      //DATA FETCHING:
      sen1=phm();
      sen2=wtemp();
      sen3 = digitalRead(pirSensor);

      
      Serial.print("pH:");
      Serial.println(sen1);
      Serial.print("Temperature:");
      Serial.println(sen2);
      Serial.print("PIR:");
      Serial.println(sen3);
      
      
      //Sending data to nodemcu:

here all 3 sensors data is pass through nodemcu one by one
      float data1=sen1;
      if(Serial3.available()>0)
      {
       char c=Serial3.read();
       if(c=='s')
        {
         Serial3.print(data1);          
         Serial3.print('\n');
         Serial3.flush();
        } 
      }

      float data2=sen2;
      if(Serial3.available()>0)
      {
       char p=Serial3.read();
       if(p=='k')
        {
         Serial3.print(data2);        
         Serial3.print('\n');
         Serial3.flush();
        } 
      }

      int data3=sen3;
      if(Serial3.available()>0)
      {
       char m=Serial3.read();
       if(m=='l')
        {
         Serial3.print(data3);        
         Serial3.print('\n');
         Serial3.flush();
        } 
      }
 delay(1000);
}







code description:

I have used the Arduino Mega 2560 as main processor of the device which is mainly a microcontroller board based on the ATmega2560.This board has 54 digital input/output pins (15 can be used as PWM outputs), 16 analog inputs, 4 UARTs (hardware serial ports), a 16 MHz crystal oscillator, a USB connection, power jack, ICSP header, and a reset button. I have left a port for a wireless connection setup in the board and have used DPM for running the board in a minimum power required.

For pH measuring sensor unit of the device for I have used Analog pH Sensor module V2 which is specifically designed to measure the pH value (a value that measures the acidity or alkalinity of the solution) of any solution. The onboard voltage regulator chip operates at a wide voltage supply of 3.3V to 5.5V which is compatible with 5V and 3.3V main control board. These features include hardware filtered output signal, low jitter, and uniform size and connector, convenient for the design of mechanical structures.
 
I have used DS18B20 as temperature measuring unit for any aquatic environment which is small temperature sensor with a built in 12bit Analog to digital converter. It can be easily connected to Arduino digital input with 3 output to the processor board. The sensor communicates with a one-wire bus built in the device and requires little power consumption in the way of additional components.
iv.	PIR motion sensor HC-SR501 
For detecting motion underwater, I have used PIR (passive infrared) sensor which allow to detect whether any movable object (like human, any fish or any warm body) which has temperature above absolute zero can be detected within a counted range. They are small, inexpensive, low-power, easy to use and convenient. 








code output:



 code output is shown in picture 1.jpg file.

