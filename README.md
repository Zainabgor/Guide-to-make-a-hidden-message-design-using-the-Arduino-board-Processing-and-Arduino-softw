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
##### You simply need to connect the 2 end pins of the potentiometer to the 5V and ground. The middle pin of the potentiometer meter to A0. 
![](https://padlet-uploads.storage.googleapis.com/967583516/94eecccddfb219a179a9db388d513ccc/20211124_221103.jpg) 

## Step 2: Open the Arduino software and copy the code that's below and run it 
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

##### Note: Ensure that the right port and board is selected in Arduino
![](https://padlet-uploads.storage.googleapis.com/967583516/44d0bc788403f0c91d77e52519212af8/user_guide_for_setting_board_and_port_.png) 


## Step 3: Open the Processing software and copy the code that's below
##### each code step has an explanation next to it 

```javascript
import processing.serial.*;    // Importing the serial library to communicate with the Arduino 

Serial myPort;      // Initializing a vairable named 'myPort' for serial communication

float background_color ;   // Variable for changing the background color

PImage Asset;       // Variable for adding the image



void setup ( ) {

size (570,  300);     // Size of the serial window, you can increase or decrease as you want

Asset = loadImage("Asset.png");  // Change the image file name accordingly, ensure that the image file is the same folder as the processing file

myPort  =  new Serial (this, "COM4",  9600); // Set the com port according to which port the Arduino cirucit is connected to in the laptop  

myPort.bufferUntil ( '\n' );   // Receiving the data from the Arduino IDE

} 



void serialEvent  (Serial myPort) {

image(Asset, 0, 0); ;  // Change the image file name accordingly
  
background_color  =  float (myPort.readStringUntil ( '\n' ) ) ;  // Changing the background color according to received data

} 



void draw ( ) {

background ( 150, 50, background_color );   // Initial background color, when we will open the serial window 

Asset = loadImage("Asset.png");  ;  // Change the image file name accordingly

}
```

##### Note: the png image that I used had the file name Asset. So do remember to change the file name correctly in the code. Also, do crosscheck that the right port is written in the code (it is the 8th line of the code).

## That's all!

## Extra tips to make the png image 
##### Use the link https://anonfiles.com/Dat0p1X0ue/hidden_code_user_file_ai to download an Adobe Illustrator file that images of the five main colours seen when the potentiometer is rotated. This will help you colour your hidden code/design easily. 
##### Link to tutorial video that shows how to test if your hidden message/design works properly or not. (https://vimeo.com/650028363) 
##### (below is the screenshot image of the illustrator file) 
![](https://padlet-uploads.storage.googleapis.com/967583516/908707697964533c58821fe111c7d18d/tutorial_vid_ss.png) 
