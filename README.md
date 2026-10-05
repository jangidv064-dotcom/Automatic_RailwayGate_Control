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
<br><br>
---------------------------------------------------------------------------------------------------------------------------------------------------
# Automatic Railway Gate Control

## Project Overview

**Automatic Railway Gate Control** is an Arduino-based mini project designed to automatically control railway crossing gates when a train approaches and passes through the crossing.

The system uses **two IR sensors** to detect the movement of the train and **two servo motors** to operate the railway gates.

When the train is detected by the first IR sensor, the railway gates automatically close. After the train passes through the road-crossing section and reaches the second IR sensor, the system detects the train and automatically opens the gates again.

The main purpose of this project is to demonstrate an automatic railway crossing system that can reduce manual intervention and improve safety at railway crossings.

---

## Objectives

The main objectives of this project are:

* To design an automatic railway gate control system.
* To detect the arrival of a train using IR sensors.
* To automatically close the railway gates when a train approaches.
* To automatically open the gates after the train passes.
* To reduce the need for manual gate operation.
* To demonstrate the use of Arduino, IR sensors and servo motors in an automation project.
* To develop a simple and low-cost railway crossing prototype.

---

## Components Required

| Sr. No. | Component                                         |    Quantity | Purpose                            |
| ------- | ------------------------------------------------- | ----------: | ---------------------------------- |
| 1       | Arduino UNO                                       |           1 | Main controller of the system      |
| 2       | IR Sensor                                         |           2 | Detects the train                  |
| 3       | Micro Servo SG90                                  |           2 | Opens and closes the railway gates |
| 4       | Mini Breadboard                                   |           1 | Circuit connections                |
| 5       | Jumper Wires                                      |       1 Set | Electrical connections             |
| 6       | 2×18650 Li-ion Battery Holder with DC Barrel Jack |           1 | Power supply                       |
| 7       | USB Type-A to Type-B Cable                        |           1 | Arduino programming/power          |
| 8       | Toy Train Set                                     |           1 | Demonstration of train movement    |
| 9       | Circular Railway Track                            |           1 | Provides the train path            |
| 10      | Black/Yellow Straws                               | As required | Used as railway gate barriers      |
| 11      | Cardboard Base                                    |           1 | Base for the project model         |
| 12      | Craft Paper                                       | As required | Model decoration                   |
| 13      | Sensor Stands / Plastic Spools                    | As required | Supports the sensors               |

---

## Technologies Used

* **Arduino UNO**
* **Arduino IDE**
* **IR Sensor**
* **Micro Servo Motor (SG90)**
* Embedded C/C++ based Arduino programming
* Basic electronic circuits

---

## Working Principle

The system works using two IR sensors and two servo motors.

### Step 1 — Train Detection

When the train approaches the railway crossing, **IR Sensor 1** detects the train.

### Step 2 — Gate Closing

After receiving the signal from IR Sensor 1, the Arduino processes the input and controls the servo motors.

The railway gates are moved to the **closed position**.

### Step 3 — Train Passes the Crossing

The train continues moving along the railway track and crosses the road section.

### Step 4 — Second Sensor Detection

When the train reaches the second detection point, **IR Sensor 2** detects the train.

### Step 5 — Gate Opening

The Arduino receives the signal from IR Sensor 2 and commands the servo motors to move the gates back to the **open position**.

### Step 6 — Normal Traffic Flow

Once the gates are opened, road traffic can pass through the railway crossing again.

---

## System Flow

```text
        Train Approaches
              ↓
       IR Sensor 1 Detects
              ↓
       Arduino Processes Signal
              ↓
        Gates CLOSE
              ↓
      Train Crosses Road
              ↓
       IR Sensor 2 Detects
              ↓
       Arduino Processes Signal
              ↓
         Gates OPEN
              ↓
       Normal Traffic Flow
```

---

##  System Architecture

```text
             ┌──────────────────┐
             │    IR Sensor 1   │
             │ Train Detection  │
             └────────┬─────────┘
                      │
                      ↓
             ┌──────────────────┐
             │                  │
             │   Arduino UNO    │
             │  Main Controller │
             │                  │
             └───────┬──────────┘
                     │
              ┌──────┴──────┐
              ↓             ↓
       ┌────────────┐ ┌────────────┐
       │ Servo Motor│ │ Servo Motor│
       │   Gate 1   │ │   Gate 2   │
       └────────────┘ └────────────┘
                     ↑
                     │
             ┌───────┴─────────┐
             │   IR Sensor 2   │
             │ Train Detection │
             └─────────────────┘
```

---

## Component Functions

### Arduino UNO

Arduino UNO acts as the **main controller** of the project. It receives signals from the IR sensors and controls the servo motors according to the detected train movement.

### IR Sensors

Two IR sensors are used for train detection.

* **IR Sensor 1:** Detects the approaching train and starts the gate-closing operation.
* **IR Sensor 2:** Detects the train after it crosses the road section and starts the gate-opening operation.

### Servo Motors

Two Micro Servo SG90 motors are used to operate the railway gates.

They rotate the gates between their open and closed positions according to the commands received from the Arduino.

### Breadboard

The mini breadboard is used to make the circuit connections easier without soldering.

### Jumper Wires

Jumper wires are used to connect the Arduino, IR sensors, servo motors and power supply.

---

## Software

The project uses the **Arduino IDE** for programming the Arduino UNO.

The Arduino program continuously monitors the IR sensors.

Basic logic:

```text
IF Sensor 1 detects train
    → Close railway gates

IF Sensor 2 detects train
    → Open railway gates
```

---

## Algorithm

1. Start the system.
2. Initialize Arduino pins, IR sensors and servo motors.
3. Keep the railway gates in the open position.
4. Continuously monitor IR Sensor 1.
5. If IR Sensor 1 detects a train:

   * Command the servo motors.
   * Close both railway gates.
6. Continue monitoring the second sensor.
7. If IR Sensor 2 detects the train:

   * Command the servo motors.
   * Open both railway gates.
8. Return to the monitoring state.
9. Repeat the process continuously.

---

## Features

* Automatic railway gate operation.
* Train detection using IR sensors.
* Automatic gate closing and opening.
* Arduino-based control.
* Simple and low-cost prototype.
* Easy to understand and implement.
* Reduces manual intervention.
* Suitable for educational and demonstration purposes.

---

##  Advantages

* Reduces the need for manual rail
