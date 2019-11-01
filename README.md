# CinderellaDress

#include <Adafruit_NeoPixel.h>

#define CE_PIN 9
#define CSN_PIN 10

int PIN=6;
int NUMPIXELS=600;
int PIXELPERLINE=60;
int LINES=10;

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

void setup() {
  // put your setup code here, to run once:
  pixels.begin();
  pixels.show();
}

void loop() {
  // put your main code here, to run repeatedly:
  degradado(pixels.Color(15, 35, 61), 100); //Los Leds se encienden consecutivamente desdel 59 hasta el 0
  //degradado(pixels.Color(31, 70, 122), 100); //Los Leds se encienden consecutivamente desdel 59 hasta el 0
  delay(1500);
  //degradado(pixels.Color(0, 10, 255), 100); //Los Leds se encienden consecutivamente desdel 59 hasta el 0
  //delay(1500);
  pixels.fill(pixels.Color(0, 0, 0), 0, NUMPIXELS);
  pixels.show();
  delay(1500);  

   theaterChase(pixels.Color(20,20,255), 50);//Los leds se encienden y apagan alternativamente uno si y uno no


  
  //colorYair(pixels.Color(0, 0, 100), 1);
  //delay(500);
  //pixels.fill(pixels.Color(0, 0, 0), 0, NUMPIXELS);
  //delay(1500);
  
  
}
