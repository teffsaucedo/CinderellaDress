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
   
  //colorTeff(pixels.Color(0, 0, 100), 1);
  //delay(500);
  //pixels.fill(pixels.Color(0, 0, 0), 0, NUMPIXELS);
  //delay(1500);
}
void colorTeff(uint32_t c, uint8_t wait) {
  for(uint16_t i=0; i<=NUMPIXELS; i++) {
    pixels.setPixelColor(i, c);
    pixels.show();
    delay(wait);
  }
}
void porLineas(uint32_t c, uint8_t wait) {
    for(int j=0; j<=LINES; j++){
      for(int i=1; i<=PIXELPERLINE; i++){
          pixels.setPixelColor(i + j*PIXELPERLINE - 1, c);
      }
      pixels.show();
      delay(wait);
    }
}
void degradado(uint32_t c, uint8_t wait) {
  for(uint16_t i=0; i<=PIXELPERLINE; i++) {

    for(int j=1; j<=LINES; j++){
      if (j % 2 == 0){
        //Es linea par
        pixels.setPixelColor(j*PIXELPERLINE - 1 - PIXELPERLINE + i, c);
      }else{
        //Es linea impar
        pixels.setPixelColor(j*PIXELPERLINE - 1 - i, c);
      }  
    }
    
    pixels.show();
    delay(wait);
  }
}

void theaterChase(uint32_t c, uint8_t wait) {
  for (int j=0; j<10; j++) {  //do 10 cycles of chasing
    for (int q=0; q < 3; q++) {
      for (int i=0; i < pixels.numPixels(); i=i+3) {
        pixels.setPixelColor(i+q, c);    //turn every third pixel on
      }
      pixels.show();

      delay(wait);

      for (int i=0; i < pixels.numPixels(); i=i+3) {
        pixels.setPixelColor(i+q, 0);        //turn every third pixel off
      }
    }
  }
}

