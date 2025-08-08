# How-to-make-a-simple-quadcopter-with-AVR-


<img width="2417" height="1629" alt="image" src="https://github.com/user-attachments/assets/d5c7f0b7-92a6-4433-93c2-b1917617401c" />

<img width="448" height="280" alt="image" src="https://github.com/user-attachments/assets/a26c61bf-4fda-4ea8-9304-8ebbc82e813a" />




This project involves designing and building a simple quadcopter using an ATmega64 microcontroller. An MPU6050 sensor sends orientation data via I²C, which is processed by a PID algorithm to maintain stability. PWM signals control four brushless motors through ESCs, while commands are received via a wireless module.
Project Description: Building a Simple Quadcopter Using AVR Microcontroller

This project involves designing and building a small quadcopter controlled by an AVR family microcontroller (such as ATmega328P or ATmega32 or atmega64). The quadcopter consists of four brushless DC motors arranged in an “X” or “+” configuration, each driven by an Electronic Speed Controller (ESC). The AVR microcontroller reads data from motion sensors (gyroscope and accelerometer, typically via an MPU6050 module) to maintain stability through a PID control algorithm. User control is achieved through a wireless communication module (e.g., 2.4 GHz RC receiver or NRF24L01). The AVR outputs PWM signals to the ESCs to adjust motor speeds, allowing for lift, movement, and rotation.

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


General Project Overview:
At the beginning, we activated the interrupts in the first section. Then, in the init part, we defined the input and output values.
In this project, we need interrupts from 0 to 5, which we activate using the ORG directive.




<img width="458" height="494" alt="image" src="https://github.com/user-attachments/assets/3ee0e249-d59f-4243-bd32-73abdd961c3c" />


The stack pointer setup, interrupt enabling, and the working mode of the interrupts are defined here. To calculate 250 milliseconds for interrupts 2 and 3, we have set the value of TCNT0 to 6.



<img width="524" height="525" alt="image" src="https://github.com/user-attachments/assets/85cd09c0-d22d-44d8-920c-4b05bfd61820" />




General Overview of the Project:
At the beginning, we activated the interrupts in the first section. Then, in the initialization part, we defined the input and output values. In this project, we require interrupts from 0 to 5, which are activated using the ORG directive.

The configuration of the stack pointer, enabling of interrupts, and the working mode of the interrupts are defined here. To calculate 250 milliseconds for interrupts 2 and 3, we have set the TCNT0 register to 6.

In this section, we first activated Timer 0 and set the output ports by assigning them a value of 1, indicating output mode. It is worth mentioning that PORTD and PORTE are used in the scoring section to display the position.





<img width="593" height="533" alt="image" src="https://github.com/user-attachments/assets/d124ce63-be33-40bf-87a7-31d7f30aaf7c" />





We also set registers 17 to 30 to zero so that they can be used in the main code without containing any previous values.



<img width="939" height="526" alt="image" src="https://github.com/user-attachments/assets/f05913e3-0a5e-4453-b581-1ceb0a73fbe7" />




The initial values that the quadcopter must take were stored in the registers, and the interrupts were set.




<img width="905" height="185" alt="image" src="https://github.com/user-attachments/assets/f58f0853-13bb-4342-a266-db9a53c13903" />




Interrupts:
In interrupts 0 and 1, we performed shift operations (which act as a buffer). In interrupt 0, we used a logical AND with 0, and in interrupt 1, we used a logical OR with 1.

<img width="975" height="311" alt="image" src="https://github.com/user-attachments/assets/40d9a1c0-c46e-41c6-b132-b903a0f13d16" />




In interrupts 4 and 5, the zero and back interrupts are for direction 1 and 2 speed, and 4 and 5 are for height adjustment:




<img width="955" height="497" alt="image" src="https://github.com/user-attachments/assets/2487e38b-3c07-4df9-be77-0c95a23b3e81" />





Timer Zero: In the timer, we have set two registers for the counter, one for every two seconds and the other for every three seconds to back up the relevant interrupts:




<img width="975" height="313" alt="image" src="https://github.com/user-attachments/assets/2ea3dc65-33e1-4129-8ede-068f04997516" />




In the Check Direction section, the direction for checking the buffer is determined based on the corresponding values:




<img width="614" height="641" alt="image" src="https://github.com/user-attachments/assets/87aba0f4-7bf9-434a-baa3-144379296004" />




If it matches the corresponding code, it enters one of the direction rings:




<img width="484" height="660" alt="image" src="https://github.com/user-attachments/assets/49c37dfe-201e-45db-b30b-4796608282ef" />




This section is related to speed, so we enter this section of the program every three seconds. If the corresponding password is OK, the processor decides to reduce or increase the speed:




<img width="975" height="538" alt="image" src="https://github.com/user-attachments/assets/968f6e24-5706-4c69-8e7e-dd432579677e" />




In this section of the code, the speed is increased, which is checked in each section to ensure that the value does not exceed 20, and if it does, it goes to the max speed section to get the value 20:




<img width="399" height="517" alt="image" src="https://github.com/user-attachments/assets/93ae4c6e-171c-4b6a-9189-7ac8e6a6b715" />




In this section, it is also used to reduce speed. In each section, it is checked so that the value is not 0 or less than 0. That is why we have given zero in the clear speed section:




<img width="686" height="600" alt="image" src="https://github.com/user-attachments/assets/335031ea-98cb-49c5-81e5-480d20af7dc6" />




In this section, we have used a seven-segment display to display the speed. First, we want to understand that it is a single digit. If it is not, we go to the digit part of the digit. We also want our speed not to be more than twenty. We compare it with 10 digits and go to the label twenty. The possible values are 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20:




<img width="522" height="547" alt="image" src="https://github.com/user-attachments/assets/bac8e3f6-b7b9-48db-a26d-1414bfad1418" />




Height adjustment: In this section, we compare the code and then, based on the entered code, we understand how much to add to the height:




<img width="508" height="847" alt="image" src="https://github.com/user-attachments/assets/63d28a52-86c1-43b2-87e6-cacf55d993bf" />




In the loops, it is checked that if it is greater than 250, it goes to the max high section until the value 250 is set there:




<img width="321" height="119" alt="image" src="https://github.com/user-attachments/assets/680774f4-788c-402c-a33e-8abefeb44026" />




In the tobcd section, we display the height value by first subtracting 100 from the height to obtain the hundreds value. Then the remainder goes to the next section and 10 is subtracted sequentially to obtain the tens value. The remainder is our units value. Then in the phase3 section, by shifting, we display the tens as bcd in the 4 most significant bits of portc and the units as bcd in the 4 least significant bits. We do the same to display the hundreds:




<img width="619" height="850" alt="image" src="https://github.com/user-attachments/assets/9acf1650-0b59-4880-aeae-e393ff7b5329" />

<img width="495" height="210" alt="image" src="https://github.com/user-attachments/assets/2506ec43-a371-4f7e-840e-24179249fa0a" />


In this section, we have simulated the project in the Proteus program:


<img width="975" height="642" alt="image" src="https://github.com/user-attachments/assets/0e0f36a4-cbe8-4761-b0a4-02fe575ac8c5" />






And finally, we have implemented part of the project in practice:





<img width="947" height="679" alt="image" src="https://github.com/user-attachments/assets/f20a8ecd-ab7b-4dbd-b8a1-63fa54780f50" />



Finally, I hope you enjoyed this project. This project was programmed in Dr. Dalir's microprocessor and assembly language course at Khajeh Nasir Tosi University in Tehran. It was a very difficult and breathtaking project that we finally implemented in the JTag programmer. You can download the entire code file in the code section.
























