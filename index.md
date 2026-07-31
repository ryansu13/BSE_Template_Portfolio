Chameleon Light

A light that imitates nature. The chameleon light take the greatest RGB value of the object held to its color sensor and the corresponding LED flashes that color. 

| **Name** | **School** | **Area of Interest** | **Grade** |
| Ryan S | Stratford Preparatory | Electrical Engineering | Eight grader

![Headstone Image](logo.svg)

FINAL MILESTONE
My final milestone was to get the wires and breadboards so that they could fit nicely in the 3d printed box, along with my modifications. I also wanted to increase the amount of colors that could be displayed in the code. Before that, I added yellow to the color portfolio and built the 3D shell for the circuits. My biggest challenge was getting the code to work because there were so many aspects that had to be solved. My greatest accomplishment was getting the code to work, because it was such a long and challenging process. I learned a lot about the internals of wiring and Arduino's. I hope to learn about how the color sensor works and the code behind it. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

- I learned how to code in Arduino-code and learned how to wire up LEDS.
- I hope to learn about the insides of the Arduino Uno and the software code. 



# Second Milestone


<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

I got the 3D print to work, which was a crucial part of my goal, to ensure that the lighting system wouldn't get damaged. I was surprised when the it was hard to move the 3D print axes and I tried a five yellow bulbs and they all didn't work. I got both of these issues to work in the end, though. Now I just need to combine them for my final milestone. 

# First Milestone


<iframe width="560" height="315" src="https://www.youtube.com/watch?v=GoMx1A4RzwE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

The breadboard will connect the LEDs and the color sensors, which will be supplied with power from an Arduino Uno. So far I have gotten the code to work, which is: if an object is held to the sensor, it takes the greatest RGB value and the corresponding light turns on. I will add more lights, which makes it more difficult and will 3D print a casing. My plan is to finish the software, then move onto a 3D print, and assembling everything. 

# Schematics 
<img width="1448" height="1204" alt="Screenshot 2026-07-24 163242" src="https://github.com/user-attachments/assets/ab12bbae-8aba-4994-84e7-3a27a9bd8e4d" />
<img width="1614" height="1138" alt="Screenshot 2026-07-24 134407" src="https://github.com/user-attachments/assets/d56ce55b-9d93-4995-995f-59ae008c9ede" />

<img width="1694" height="1054" alt="Screenshot 2026-07-27 132413" src="https://github.com/user-attachments/assets/46eea78e-dc3b-4d0c-be78-5a3936d9e9fe" />


# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
#include <Adafruit_NeoPixel.h>  
#ifdef __AVR__  
#include <avr/power.h>  
#endif  
   
#define PIN      9  
   
#define NUMPIXELS 5  
   
Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);  
   
int delayval = 333; // delay  
 
#define S0 4
#define S1 5
#define S2 6
#define S3 7
#define sensorOut 8
 
int frequency = 0;
int Red, Green, Blue;

int redFreq, yellowFreq, greenFreq, blueFreq; 

int redPin = 13; 
int yellowPin = 10; 
int greenPin = 11; 
int bluePin = 2; 
int currentPin; 
int rightPin; 

void setup() {
  pinMode(S0, OUTPUT);
  pinMode(S1, OUTPUT);
  pinMode(S2, OUTPUT);
  pinMode(S3, OUTPUT);
  pinMode(sensorOut, INPUT);
  pinMode(redPin, OUTPUT); 
  pinMode(yellowPin, OUTPUT); 
  pinMode(greenPin, OUTPUT); 
  pinMode(bluePin, OUTPUT); 
 
  digitalWrite(S0,HIGH);
  digitalWrite(S1,LOW);
 
  Serial.begin(9600);
  pixels.begin(); 
}
 
void loop() {
  digitalWrite(S2,LOW);
  digitalWrite(S3,LOW);
  frequency = pulseIn(sensorOut, LOW);
  frequency = map(frequency, 25,72,255,0);
  if (frequency < 0) {
    frequency = 0;
  }
  if (frequency > 255) {
    frequency = 255;
  }
  Red= frequency;
  redFreq = Red; 
  Serial.print("R= ");
  Serial.print(Red);
  Serial.print("  ");
  delay(100);
 
  digitalWrite(S2,HIGH);
  digitalWrite(S3,HIGH);
  frequency = pulseIn(sensorOut, LOW);
  frequency = map(frequency, 30,90,255,0);
  if (frequency < 0) {
    frequency = 0;
  }
  if (frequency > 255) {
    frequency = 255;
  }
  Green = frequency;
  greenFreq = Green; 
  Serial.print("G= ");
  Serial.print(Green);
  Serial.print("  ");
  delay(100);
 

  digitalWrite(S2,LOW);
  digitalWrite(S3,HIGH);
  frequency = pulseIn(sensorOut, LOW);
  frequency = map(frequency, 25,70,255,0);
  if (frequency < 0) {
    frequency = 0;
  }
  if (frequency > 255) {
    frequency = 255;
  }
  Blue = frequency;
  blueFreq = Blue; 
  Serial.print("B= ");
  Serial.print(Blue);
  Serial.println("  ");
  pixels.setPixelColor(0, pixels.Color(Red,Green,Blue)); 
  pixels.setBrightness(64);  
  pixels.show();
  delay(100);

  if (redFreq > 120 && greenFreq < 70 && blueFreq < 70){
    rightPin = redPin; 
    digitalWrite(yellowPin, LOW);
    digitalWrite(greenPin, LOW);
    digitalWrite(bluePin, LOW);
    digitalWrite(redPin, HIGH); 
  }
  else if (redFreq > 90 && greenFreq > 90 && blueFreq < 70){
    rightPin = yellowPin; 
    digitalWrite(redPin, LOW); 
    digitalWrite(bluePin, LOW); 
    digitalWrite(greenPin, LOW); 
    digitalWrite(yellowPin, HIGH);
  }
  else if (greenFreq > 70 && redFreq < 70 && blueFreq < 70){
    rightPin = greenPin; 
    digitalWrite(redPin, LOW); 
    digitalWrite(yellowPin, LOW); 
    digitalWrite(bluePin, LOW); 
    digitalWrite(greenPin, HIGH);
  }
  else if (blueFreq > 70 && greenFreq < 70 && redFreq < 70){
    rightPin = redPin; 
    digitalWrite(redPin, LOW); 
    digitalWrite(yellowPin, LOW);
    digitalWrite(greenPin, LOW);
    digitalWrite(bluePin, HIGH); 
  }

  if(currentPin != rightPin){
    digitalWrite(currentPin, LOW); 
    currentPin = rightPin; 
    digitalWrite(rightPin, HIGH);
  }

  currentPin = rightPin; 

}
```

Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
| Arduino UNO | It acts like the motherboard to my project | $5 | <a href="https://store-usa.arduino.cc/collections/uno"> Link </a> |
| Color Sensor | Sensing color | $9 | <a href="https://www.amazon.com/arduino-color-sensor/s?k=arduino+color+sensor"> Link </a> |
| RGB LED | Shows color | $5 | <a href="https://www.digikey.com/en/products/detail/adafruit-industries-llc/4203/10130502"> Link </a> |
| Breadboard | It connects the bulbs.  | $3 | <a href="https://www.walmart.com/ip/Solderless-Breadboard-400-Tie-Points-2-Power-Rails-3-3-x-2-1-x-0-3-Inches/742836011?wmlspartner=wlpa&selectedSellerId=594&veh=seo_fpl&cn=google"> Link </a> |
| Jumper wires | Connects everything.  | $4 | <a href="https://www.walmart.com/ip/Jumper-Wire-Cable-3-X-40-Pcs-Each-20-Cm-Dupont-Breadboard-Cables-In-1-Male-To-Female-Male-Female-For-Arduino-Raspberry-Pi/15611404788?wmlspartner=wlpa&selectedSellerId=101622314"> Link </a> |
