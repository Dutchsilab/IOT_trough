## Overview 101

An Arduino project to detect pet food inside a bowl. If the bowl is empty the Arduino will send a message
to the device to tell its empty or needs a refill. The Ultrasonic Sensor HC-SR04 will do all the heavy work!

### Prerequisites

To get started, you need an Arduino board and the Arduino program to get started.

```
- Windows 8 or 10, MacOS & Linux.
- A working Arduino board.
- You need the component 'Ultrasonic Sensor HC-SR04' [Check it here](https://howtomechatronics.com/tutorials/arduino/ultrasonic-sensor-hc-sr04/)
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
