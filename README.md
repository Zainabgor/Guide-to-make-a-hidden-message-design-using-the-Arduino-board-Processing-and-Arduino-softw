# Guide to make a hidden message/design using the Arduino board, Processing software and Arduino software 

## The logic (how it works) 
##### The Arduino and the Processing will communicate with each other through serial communication. When you manually rotate the potentiometer it will send a reading to Aridino which will convert it into an integer number between 0 to 225. Processing will change the colour in the serial window that corresponds to the number reading that it received. 
##### Since the whole process only affects the background colour of the serial window you can place an image with a transparent background (png) on top of it. If your change the colour of certain parts of the image according to the colours in the serial window you can hide a message that will only be read on depending on the movement of the potential meter.  

## Things you need-
* Arduino board
* 3 jumper wires
* a potentiometer 
* a USB cable to connect the Arduino circuit to the laptop
* Download the Arduino software using the following link https://www.arduino.cc/en/software
* Download the Processing software using the following link  https://processing.org/
(both the software are free ;)

## Step 1: make the Arduino circuit 
You simply need to connect the 2 end pins of the potentiometer to the 5V and ground. The middle pin of the potentiometer meter to A0. 
![](https://padlet-uploads.storage.googleapis.com/967583516/94eecccddfb219a179a9db388d513ccc/20211124_221103.jpg) 

## Step 2: Open the Arduino software and copy the code below 
##### each code step has an explanation next to it 

```javascript

int pot_pin = A0;   // Initializing the Potentiometer pin

int pot_output;     // Declaring a variable for potentiometer output

void setup ( ) {

Serial.begin(9600);       // Starting the serial communication at 115200 baud rate

} 

void loop ( ) { 

pot_output = analogRead (pot_pin); // Reading from the potentiometer

int mapped_output = map (pot_output, 0, 1023, 0, 255); // Mapping the output of potentiometer to 0-255 to be read by the Processing IDE 

Serial.println (mapped_output);     // Sending the output to Processing IDE

} 
```
## Step 2: Open the Processing software and copy the code below
