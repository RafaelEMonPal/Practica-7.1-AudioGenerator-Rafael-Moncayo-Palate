# Practica-7.1-AudioGenerator-Rafael-Moncayo-Palate

## Codi de la Pràctica 

```cpp

#include <Arduino.h>
#include "AudioGeneratorAAC.h"
#include "AudioOutputI2S.h"
#include "AudioFileSourcePROGMEM.h"
#include "sampleaac.h"
AudioFileSourcePROGMEM *in;
AudioGeneratorAAC *aac;
AudioOutputI2S *out;
void setup(){
Serial.begin(115200);
in = new AudioFileSourcePROGMEM(sampleaac, sizeof(sampleaac));
aac = new AudioGeneratorAAC();
out = new AudioOutputI2S();
out -> SetGain(5);
out -> SetPinout(26,25,22);
aac->begin(in, out);
}

void loop(){
  if (aac->isRunning()) {
    aac->loop();
  } else {
  aac -> stop();
  Serial.printf("Sound Generator\n");
  delay(1000);
  }
}

```

## Explicació de la pràctica

Les llibreries que utilitzarem per aquest programa és l'audio i el sampleaac.h. Començarem amb la declaració de la font on treurem el so, el generador i el output de sortida com a punters. i en el setup declara la entrada in com un objecte nou de Audio File Source PROGMEM amb parametres del sampleaac. 
En el void Loop tindrem en bucle la funció de aac en la que comprovarem si esta funcionant i si ho esta reproduirà un so, però si no: pararà el procés amb la inconveniencia de que tenim un serial.print que no pararà i per tant el que pasarà serà que el àudio es reproduirà 1 vegada pero per pantalla no pararà de sortir "Sound Generator".
