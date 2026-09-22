# Automatic_RailwayGate_Control
For MPCA
<br>
#include <Servo.h>

Servo servo1;
Servo servo2;

// IR Sensor Pins
const int sensor1 = 2;
const int sensor2 = 3;

// Servo Pins
const int servo1Pin = 9;
const int servo2Pin = 10;

// Motor status
bool motorRunning = false;

void setup() {
  pinMode(sensor1, INPUT);
  pinMode(sensor2, INPUT);

  servo1.attach(servo1Pin);
  servo2.attach(servo2Pin);

  // Initially STOP both servos
  servo1.write(90);
  servo2.write(90);

  delay(1000);
}

void loop() {

  // Sensor 1 detects train → START spinning
  if (digitalRead(sensor1) == LOW && motorRunning == false) {

    servo1.write(360);    // Continuous rotation
    servo2.write(360);  // Opposite direction

    motorRunning = true;

    delay(500);
  }

  // Sensor 2 detects train → STOP spinning
  if (digitalRead(sensor2) == LOW && motorRunning == true) {

    servo1.write(90);   // STOP
    servo2.write(90);   // STOP

    motorRunning = false;

    delay(500);
  }
}
<br>
