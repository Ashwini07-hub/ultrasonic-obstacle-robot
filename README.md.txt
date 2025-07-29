# 🤖 Obstacle Avoidance Robot Using Ultrasonic Sensor

This project presents a simple autonomous robot capable of detecting and avoiding obstacles using an ultrasonic sensor and motor control via an L298N H-Bridge motor driver. The robot is built on a stable chassis and powered by a microcontroller (e.g., Arduino Uno).

---

## 🔧 Hardware Setup

- Construct a stable robot chassis that holds all components: microcontroller, ultrasonic sensor, L298N motor driver, motors, wheels, and power supply.
- Ensure the components are securely fixed and the chassis provides proper balance for movement.

---

## 🔌 Sensor Integration

- **Ultrasonic Sensor (HC-SR04)** is interfaced with the Arduino.
- It continuously measures the distance to obstacles in the robot’s path using time-of-flight echo detection.
- The sensor data is processed in real-time to identify nearby obstacles.

---

##⚙️ Motor Control

- **L298N H-Bridge motor driver** is used to drive the two DC motors.
- The direction and speed of the motors are controlled through Arduino PWM and digital pins.
- Motor speed is dynamically adjusted based on the proximity of obstacles.

---

## 🧠 Obstacle Avoidance Logic

- The robot reads ultrasonic distance data continuously.
- If an obstacle is detected within a specified range (e.g., < 20 cm), the robot:
  - Stops
  - Turns left or right based on a predefined strategy
- If the path is clear, the robot continues moving forward.

---

## 🧩 Components Used

| Component              | Quantity |
|------------------------|----------|
| Arduino Uno            | 1        |
| HC-SR04 Ultrasonic Sensor | 1    |
| L298N Motor Driver     | 1        |
| BO DC Motors (100 RPM) | 2        |
| Wheels + Castor        | 2 + 1    |
| Robot Chassis          | 1        |
| 9V/12V Battery Pack    | 1        |
| Jumper Wires           | As needed |
| Breadboard (optional)  | 1        |

---

## 🧠 Sample Arduino Code (Simplified)

```cpp
#include <NewPing.h>

#define TRIG_PIN 9
#define ECHO_PIN 10
#define MAX_DISTANCE 200

NewPing sonar(TRIG_PIN, ECHO_PIN, MAX_DISTANCE);

#define ENA 5
#define IN1 6
#define IN2 7
#define IN3 8
#define IN4 11
#define ENB 3

void setup() {
  pinMode(IN1, OUTPUT); pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT); pinMode(IN4, OUTPUT);
  pinMode(ENA, OUTPUT); pinMode(ENB, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int distance = sonar.ping_cm();
  Serial.print("Distance: ");
  Serial.println(distance);

  if (distance > 0 && distance < 20) {
    // obstacle detected
    turnRight();
    delay(500);
  } else {
    moveForward();
  }
}

void moveForward() {
  digitalWrite(IN1, HIGH); digitalWrite(IN2, LOW);
  digitalWrite(IN3, HIGH); digitalWrite(IN4, LOW);
  analogWrite(ENA, 200); analogWrite(ENB, 200);
}

void turnRight() {
  digitalWrite(IN1, LOW); digitalWrite(IN2, HIGH);
  digitalWrite(IN3, HIGH); digitalWrite(IN4, LOW);
  analogWrite(ENA, 200); analogWrite(ENB, 200);
}


---

👩‍🎓 Project Information
Project Title: Obstacle Avoidance Robot using Ultrasonic Sensor
Academic Year: 2023-24
Submitted By: Ashwini Ravasaheb Mangasuli
Department: Electronics & Telecommunication Engineering
College: Sinhgad College of Engineering, Pune


