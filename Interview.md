## 1. What is an embedded system?
- An Embedded System is a special-purpose computer system designed to perform a specific dedicated function within a larger system.
- It consists of hardware + software (firmware) that work together to perform a particular task.
  ### Components of Embedded System
  #### Hardware:
  - Microcontroller or Microprocessor (e.g., ARM Cortex, AVR, PIC)
  - Memory (RAM, ROM, Flash)
  - Input/Output interfaces (GPIO, ADC, UART, SPI, I²C)
  - Sensors and actuators
  #### Software (Firmware):
  - Written in C/C++ or assembly
  - Often runs on RTOS (Real-Time Operating System) like FreeRTOS, VxWorks, or bare-metal.
- It’s a combination of hardware and software designed for a specific task.
- Uses microcontrollers or microprocessors.
- Often works in real-time and has resource constraints (limited CPU, memory).
- Found everywhere — in automobiles, medical devices, consumer electronics, and IoT.
- Can be standalone or connected (networked).

## 2. Explain types of embedded system?
### Standalone Embedded Systems
#### Definition
- A Standalone Embedded System operates independently and does not rely on any external system to perform its task.
- It takes input, processes it, and gives output — all within itself.
#### Characteristics
- Works without a host (PC/server)
- Uses input devices (keypad, sensors)
- Generates output (display, actuator, etc.)
- Runs a single, fixed function
#### Examples
- Digital Calculator
- Washing Machine Controller
- Microwave Oven
- MP3 Player
### Real-Time Embedded Systems
#### Definition
- A Real-Time Embedded System must respond to inputs or events within a specific time limit (deadline).
- Delays or missed deadlines can cause system failure or danger.
- 
  | Type               | Description                    | Example                      |
| ------------------ | ------------------------------ | ---------------------------- |
| **Hard Real-Time** | Must meet deadlines every time | Airbag system, Pacemaker     |
| **Soft Real-Time** | Occasional delay acceptable    | Multimedia systems, Printers |
