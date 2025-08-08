# How-to-make-a-simple-quadcopter-with-AVR-
This project involves designing and building a simple quadcopter using an ATmega64 microcontroller. An MPU6050 sensor sends orientation data via I²C, which is processed by a PID algorithm to maintain stability. PWM signals control four brushless motors through ESCs, while commands are received via a wireless module.
Project Description: Building a Simple Quadcopter Using AVR Microcontroller

This project involves designing and building a small quadcopter controlled by an AVR family microcontroller (such as ATmega328P or ATmega32). The quadcopter consists of four brushless DC motors arranged in an “X” or “+” configuration, each driven by an Electronic Speed Controller (ESC). The AVR microcontroller reads data from motion sensors (gyroscope and accelerometer, typically via an MPU6050 module) to maintain stability through a PID control algorithm. User control is achieved through a wireless communication module (e.g., 2.4 GHz RC receiver or NRF24L01). The AVR outputs PWM signals to the ESCs to adjust motor speeds, allowing for lift, movement, and rotation.

Main components:

AVR microcontroller board (e.g., Arduino Nano with ATmega328P)

4 × Brushless DC motors + propellers

4 × ESCs (Electronic Speed Controllers)

MPU6050 (Gyroscope + Accelerometer)

Wireless receiver (e.g., NRF24L01 or RC receiver)

Li-Po battery (e.g., 3S 11.1V)

Quadcopter frame

Key functions:

Sensor data reading via I²C

PID algorithm for flight stability

PWM generation to control motor speeds

Wireless communication for control signals

Outcome:
A functional quadcopter capable of stable flight under manual remote control, with the AVR microcontroller handling sensor fusion and motor control.
