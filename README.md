# Acelerometro-ADXL335
Este proyecto consiste en tomar medidas de un acelerometro analogico en la plataforma de Arduino, el cual estará asignado como PWM a la posición del servomotor.

A continuación se mostrará el código


//Pines analogicos de lectura


 const int xPin = 0;    
 
 const int yPin = 1;
 
 const int zPin = 2;
 

// Valores mínimos y máximos del acelerometro en reposo


 int minVal = 265;     
 
 int maxVal = 402;
 

// Para guardar los valores calculados

 double x;    
 
 double y;
 
 double z;

void setup ( ) {

 Serial.begin(9600);
 
 }

void loop ( ) {


//Lectura de los valores analogicos del acelerometro

 int xRead = analogRead(xPin);  
 
 int yRead = analogRead(yPin);
 
 int zRead = analogRead(zPin);
 

// Mapea los valores leidos a un rango de -90 a 90 grados

 int xAng = map(xRead, minVal, maxVal, -90, 90);
 
 int yAng = map(yRead, minVal, maxVal, -90, 90);
 
 int zAng = map(zRead, minVal, maxVal, -90, 90);
 

//Conversión de radianes a grados

 x = RAD_TO_DEG * (atan2(-yAng, -zAng) + PI);
 
 y = RAD_TO_DEG * (atan2(-xAng, -zAng) + PI);
 
 z = RAD_TO_DEG * (atan2(-yAng, -xAng) + PI);
 

//Impresión en el monitor serial

 Serial.print("x: ");
 
 Serial.print(x);
 
 Serial.print("y: ");
 
 Serial.print(y);
 
 Serial.print("z: ");
 
 Serial.println(z);

delay(100);  
 }
