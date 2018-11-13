## Overview 101

An Arduino project to detect pet food inside a bowl. If the bowl is empty the Arduino will send a message
to the device to tell its empty or needs a refill. The Ultrasonic Sensor will do all the heavy work!

### Prerequisites

To get started, you need an Arduino board, the Ultrasonic Sensor HC-SR04 ([Check it here](https://howtomechatronics.com/tutorials/arduino/ultrasonic-sensor-hc-sr04/)) and the Arduino program to get started.

```
- Windows 8 or 10, MacOS & Linux.
- A working Arduino board.
- You need the component 'Ultrasonic Sensor HC-SR04'.
- The 'Arduino Program' to start coding and uploading it to the board.
- Basic understanding of Arduino coding.
- A steady WiFi connection.
- Patience :)
```

### Installing

1. Connect all the components needed to your Arduino Board ([click Here](https://www.makerspaces.com/arduino-uno-tutorial-beginners/) to see how that works!) 
2. Connect your Arduino Board using USB with your computer.
3. Fire up the program 'Arduino'. If you don't have it, [install](https://www.arduino.cc/en/Main/Software) it first.
4. Start a new 'file' and copy/paste my code from this ReadMe page.
5. Validate the code first to check if everything works correctly.
6. Before we upload the code to our Arduino, make sure the board is set to the right USB Port. You can do this by going to
Tools > Port > and select '/dev/cu.ARDUINO1'. And set the 'Upload speed' to '921600'.
6. Now, we are ready to upload the code to our Arduino board. Hit the 'arrow to the right' to start uploading.
7. If everything went according to plan, you should now have a working Arduino that detects the distance of the pet food put in the bowl.

### The Code
```
//define the pins that we will use for the first sensor.
//----------------------------------------------------------------------------------------------------------------------
#define trigPin1 D1 //Trigger pin for sensor one
#define echoPin1 D2 //Echo pin for sensor two

//define the pins that we will use for the second sensor.
//----------------------------------------------------------------------------------------------------------------------
#define trigPin2 D3 //Trigger pin for sensor one  
#define echoPin2 D4 //Echo pin for sensor two

//we'll use these variable to store and generate the data
long duration, distance, UltraSensor1, UltraSensor2;

// Char setup
char data;
// Serial setup
String SerialData="";
// Boolean setup (trigger)
int trigger = 0;

void setup()
{
Serial.begin (9600);
// setup pins first sensor
pinMode(trigPin1, OUTPUT);
pinMode(echoPin1, INPUT);         
//setup pins second sensor
pinMode(trigPin2, OUTPUT);
pinMode(echoPin2, INPUT);
}

//write the code in the loop function
void loop() 
{
SonarSensor(trigPin1, echoPin1);              // look bellow to find the difinition of the SonarSensor function
UltraSensor1 = distance;                      // store the distance in the first variable
SonarSensor(trigPin2,echoPin2);               // call the SonarSensor function again with the second sensor pins
UltraSensor2 = distance;                      // store the new distance in the second variable

while(Serial.available())
{
  delay(10);
  data=Serial.read();
  SerialData+=data;
}

//if we want to check the data manually in the console, we can write 'show' to trigger it.
if(SerialData=="show")
{
// display the distances on the serial monitor for the first sensor
//----------------------------------------------------------------------------------------------------------------------
Serial.print("distance measured by the first sensor: ");
Serial.print(UltraSensor1);
Serial.println(" cm");
//----------------------------------------------------------------------------------------------------------------------

//display the distance on the serial monitor for the second sensor
//----------------------------------------------------------------------------------------------------------------------
Serial.print("distance measured by the second sensor: ");
Serial.print(UltraSensor2);
Serial.println(" cm");
Serial.println("---------------------------------------------------------------------------------------------------------");
//----------------------------------------------------------------------------------------------------------------------
}

// We end the SerialData here because we obtained the information.
SerialData="";

if(UltraSensor1 <=5)// if the distance is less than 5 cm in the food bowl then...
{
  trigger = 1;
  send();
}
else                // else turn off
{
  trigger = 0;
}

// we'll do the same thing for second sensor.
if(UltraSensor2 <=5)
{
  trigger = 1;
  send();
}
else
{
  trigger = 0;
}
}

// Lets send the message.
void send() {
  if (trigger == 1) {
     Serial.println("The bowl is empty. Lets send a notification!");
     delay(1800000); // we delay the notification for 30minutes. Otherwise we'll spam the system for no reason...
     trigger = 0; // we reset the trigger, so the code can check if the bowl is filled or not.
  } else {
  }
}

// SonarSensor function used to generate and read the ultrasonic wave
void SonarSensor(int trigPinSensor,int echoPinSensor)//it takes the trigPIN and the echoPIN 
{
digitalWrite(trigPinSensor, LOW);// put trigpin LOW 
delayMicroseconds(2);// wait 2 microseconds
digitalWrite(trigPinSensor, HIGH);// switch trigpin HIGH
delayMicroseconds(10); // wait 10 microseconds
digitalWrite(trigPinSensor, LOW);// turn it LOW again

//read the distance
duration = pulseIn(echoPinSensor, HIGH);//pulseIn funtion will return the time on how much the configured pin remain the level HIGH or LOW; in this case it will return how much time echoPinSensor stay HIGH
distance= (duration/2) / 29.1; // first we have to divide the duration by two  
}
```
