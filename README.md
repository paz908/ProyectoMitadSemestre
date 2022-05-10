/*
  Analog Input

  Demonstrates analog input by reading an analog sensor on analog pin 0 and
  turning on and off a light emitting diode(LED) connected to digital pin 13.
  The amount of time the LED will be on and off depends on the value obtained
  by analogRead().

  The circuit:
  - potentiometer
    center pin of the potentiometer to the analog input 0
    one side pin (either one) to ground
    the other side pin to +5V
  - LED
    anode (long leg) attached to digital output 13 through 220 ohm resistor
    cathode (short leg) attached to ground

  - Note: because most Arduinos have a built-in LED attached to pin 13 on the
    board, the LED is optional.

  created by David Cuartielles
  modified 30 Aug 2011
  By Tom Igoe

  This example code is in the public domain.

  www.arduino.cc/ ... Examples/AnalogInput
*/

// ej_03_pulsador_luz_intermitente de clase

// entrada parlante como sensor
// salida LED

int pinLectura = 1;

// variables para parlante, sensor analogo
int pinParlante = A0;
int valorParlante = 0;
int valorParlanteAntes = 0;
int diferencia = 0;
int umbral = 3;

// variables para salida LED
int pinLED = 7;

// variable para estado LED
int estadoLED = 0;

int deteccionSonido = 0;

// variable para pausa de intermitencia
// const long intervalo = 1000;
// unsigned long tiempoAnterior = 0;
// unsigned long tiempoActual = 0;

void setup() {

  // declarar pin LED como salida
  pinMode(pinLED, OUTPUT);

  // prender puerto serial
  Serial.begin(9600);

}

void loop() {

  // actualizar valor antes
  valorParlanteAntes = valorParlante;

  // actualizar valor sensor parlante
  valorParlante = analogRead(pinParlante);

  // calcular diferencia
  diferencia = abs(valorParlante - valorParlanteAntes);

  // comprobar si la diferencia es mas grande que un cierto umbral
  if (diferencia > umbral) {

    Serial.println("distintos");

    deteccionSonido = 1;
  }

  else  {

    deteccionSonido = 0;

    // Serial.print(valorParlante);
    // Serial.print(", ");
    // Serial.println(valorParlanteAntes);
  }

  digitalWrite(pinLED, deteccionSonido);

}
