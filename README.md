# Guide to make a hidden message/design using the Arduino board, Processing software and Arduino software 

##### In the video below you can see how the final outcome of following this guide looks like
https://user-images.githubusercontent.com/95038832/143656161-93ffd208-f300-4fb8-a3cd-aa9d8bda967c.mp4


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
##### You simply need to connect the 2 end pins of the potentiometer to the 5V and ground (green wires). The middle pin of the potentiometer meter to A0 (black wire).
![](https://padlet-uploads.storage.googleapis.com/967583516/045064ba7ad2c4a30436c7dca41210da/circuit_image_for_open_source_file.jpg) 

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

##### Note: if you want to use the same image that I used (the one that says 'creative computing id fun if you have patience) then use the link https://anonfiles.com/j9v175X6ud/Asset_png to download it. If not you can create your own hidden message/design in the form of a png image. There are a few helpful tips at the end of the read me file that will help you do that. REMEMBER the png image that I used had the file name Asset. So do change the file name correctly in the 7th and 12th lines of the code if you decide to create and use your own image. Also, do cross-check that the right port is written in the code (it is the 8th line of the code).

## That's all! You did it!



## Extra tips to make the png image 
##### Use the link https://anonfiles.com/Dat0p1X0ue/hidden_code_user_file_ai to download an Adobe Illustrator file that images of the five main colours seen when the potentiometer is rotated. This will help you colour your hidden code/design easily. 
##### Below is a tutorial video that shows how to test if your hidden message/design works properly or not. 
https://user-images.githubusercontent.com/95038832/143656348-e366bf20-8e27-489d-bbc7-956578688764.mp4

## Main research links used
##### Orignal code that I took and edited https://maker.pro/arduino/tutorial/how-to-make-arduino-and-processing-ide-communicate 
##### Used to understand serial communication https://littlebirdelectronics.com.au/guides/45/connect-arduino-to-processing
