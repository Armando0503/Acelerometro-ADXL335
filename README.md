# Acelerometro-ADXL335
Este proyecto consiste en tomar medidas de un acelerometro analogico en la plataforma de Arduino, el cual estará asignado como PWM a la posición del servomotor.

A continuación se mostrará el código


#include <Servo.h>

const int xPin = 0;   //ACELEROMETRO

const int yPin = 1;

const int zPin = 2;

int led2 = A3;        // Pines de lectura analógica

int led3 = A4;

// Los valores mínimos y máximos que provienen

// del acelerómetro mientras está parado

int minVal = 265;

int maxVal = 402;

// Parte del servomotor

Servo servo1;       //Crea un objeto servo que se llama servo1

int angulo = 90;    // Valor inicial del servo

// para mantener los valores calculados

double x;

double y;

double z;

void setup()
{

  Serial.begin(9600);
  
  servo1.attach(9); //Asociamos el servo a la patilla 11 de Arduino
  
}
void loop()

{// lee los valores analógicos del acelerómetro

int xRead = analogRead (xPin);

int yRead = analogRead (yPin);

int zRead = analogRead (zPin);

// convierte los valores de lectura a grados -90 a 90 - necesarios para atan2

int xAng = map (xRead, minVal, maxVal, -90, 90);

int yAng = map (yRead, minVal, maxVal, -90, 90);

int zAng = map (zRead, minVal, maxVal, -90, 90);

// Calcula valores de 360 ​​grados de la siguiente manera: atan2 (-yAng, -zAng)

// atan2 genera el valor de -π a π (radianes)

// Estamos convirtiendo los radianes a grados

x = RAD_TO_DEG * (atan2 (-yAng, -zAng) + PI);

y = RAD_TO_DEG * (atan2 (-xAng, -zAng) + PI);

z = RAD_TO_DEG * (atan2 (-yAng, -xAng) + PI);

// Genera los cálculos

Serial.print ("x: ");

Serial.print (x);

Serial.print ("y: ");

Serial.print (y);

Serial.print ("z: ");

Serial.println (z);

delay (100); // ralentizar la salida en serie

 servo1.attach(x); //Mueve el Servo a la posición definida en la variable    
 
  if(x>=180)
  
  { 
  
    digitalWrite(led2, HIGH); //el LED se prende
    
  }
  
  if(x<=0)
  
  { 
  
    digitalWrite(led2,LOW); //el LED se apaga
    
  }
  
}
 
 
 
 Integrantes:
 
 Cesár Alexander Marín Zurita
 
 Jesús Armando Gardida del Río
