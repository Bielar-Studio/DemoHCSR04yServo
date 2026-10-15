# DemoHCSR04yServo
Este proyecto es un demo de cómo interactúan juntos el HCSR04 y el Servomotor clásico

Codigo:
# include <Servo.h>

const int PIN_TRIG = 12;
const int PIN_ECHO = 11;
const int PIN_SERVO = 13;

const int LIMITE_DISTANCIA = 5;
const int TIEMPO_ABIERTO = 3500;
bool CARRO_CERCA = false;

Servo motor;

void setup() {
  pinMode(PIN_TRIG ,OUTPUT);
  pinMode(PIN_ECHO,INPUT);
  motor.attach(PIN_SERVO);
  motor.write(180);
  Serial.begin(9600);


}


void loop() {

  digitalWrite(PIN_TRIG,HIGH);
  delayMicroseconds(10);
  digitalWrite(PIN_TRIG,LOW);
  const int TIEMPO_ECHO = pulseIn(PIN_ECHO,HIGH);
  float distancia = TIEMPO_ECHO * 0.0343 / 2;
  Serial.println(distancia);
  if (distancia < LIMITE_DISTANCIA) {
  motor.write(10);
  } else {
    motor.write(90);
  }
}
