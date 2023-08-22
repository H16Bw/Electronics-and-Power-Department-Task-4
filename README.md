# Electronics-and-Power-Department-Task-4
4th task of Electronics and Power Department - Summer training program at Smart Methods

# Visitor Tracking System using PIR Sensors


 ### Tinkercad Link - Visitor Tracking System

 https://www.tinkercad.com/things/5UeZ64WMnaJ?sharecode=nasHvGiWONfCR2SnoRsZuQUp9MpXNyy3nlOCkzbhOoQ


![image](https://github.com/H16Bw/Electronics-and-Power-Department-Task-4/assets/139852537/b9eca513-f87e-43ca-b46b-44fd6531df52)



## Overview

This project demonstrates a simple visitor tracking system using Passive Infrared (PIR) motion sensors. The system keeps track of the number of visitors entering a specific area. It is commonly used in applications like entrance monitoring, occupancy tracking, and security systems.

## Hardware Components

- PIR Sensor 1 (connected to pin 2): This sensor detects motion within its range.
- PIR Sensor 2 (connected to pin 3): Another sensor used to confirm visitor entry.

## Installation

1. **Connect PIR Sensors**: Connect the PIR sensors to the specified pins on the microcontroller (Arduino or compatible).
2. **Upload Code**: Upload the provided code (`visitor_tracking_system.ino`) to the microcontroller using the Arduino IDE or similar software.

## How It Works

The system operates as follows:

1. **PIR1 Detection**:
   - When motion is detected by PIR1, the system checks if a visit is already active using the `b_PIR1_active` flag.
   - If a new visit is starting (not previously active), the system sets `b_PIR1_active` to true and checks if this is the first time crossing PIR1 (`lastRIPdetected == 0`).
   - If it's the first time, it sets `lastRIPdetected` to 1 and prints "Visit started".

2. **PIR1 Reset**:
   - If no motion is detected by PIR1 (LOW reading), the system resets the visit status (`b_PIR1_active = false`).
   - If PIR1 was previously crossed (indicating the visitor entered the monitored area), `lastRIPdetected` is set to 2.

3. **PIR2 Confirmation**:
   - Once PIR1 is crossed (`lastRIPdetected == 2`) and PIR2 detects motion, it confirms that a visitor has entered.
   - The visitor count is incremented, and `lastRIPdetected` is reset to 0.
   - The current visitor count is printed to the serial monitor.

## Usage

1. **Power On**: Ensure the system is powered on and properly connected.
2. **Monitor Visitors**: Visitors will be automatically tracked as they enter the monitored area.
3. **Serial Output**: Open the serial monitor in the Arduino IDE to see real-time visit-related information.

   
## Code Explanation

### `const int PIR1_PIN = 2;` and `const int PIR2_PIN = 3;`

These lines declare constants `PIR1_PIN` and `PIR2_PIN` and assign them the pin numbers where the PIR sensors are connected (2 and 3, respectively).

### `int visitors = 0;`

This variable holds the count of visitors who have entered the monitored area.

### `int lastRIPdetected = 0;`

This variable tracks the most recent motion detection status by the PIR sensors.

### `bool b_PIR1_active = false;`

This Boolean variable is used to determine whether PIR1 is currently detecting motion.

### `void setup() { ... }`

This function is used to set up the initial state of the program.
   - The PIR sensor pins are configured as digital inputs.
   - Serial communication is initiated with a baud rate of 9600.
   - The message "Visitors are welcome" is printed to the serial interface.

### `void loop() { ... }`

This function constitutes the main part of the program and runs in an infinite loop.

- **Checking PIR1 Sensor State**:
  - The program checks if PIR1 detects motion by reading its pin.
  - If motion is detected and PIR1 is not currently active (`b_PIR1_active == false`) and the last detection was 0 (`lastRIPdetected == 0`), the specified condition is met.
  - `b_PIR1_active` is set to true, and if it's the first time PIR1 has been crossed, `lastRIPdetected` is set to 1, and "Visit started" is printed.

- **Resetting PIR1 Sensor State**:
  - If no motion is detected by PIR1 (reading equals LOW), the state is reset by setting `b_PIR1_active` to false.
  - If PIR1 was previously crossed (indicating a visitor entered the monitored area), `lastRIPdetected` is set to 2.

- **Confirming Visitor with PIR2 Sensor**:
  - When PIR1 is crossed (`lastRIPdetected == 2`) and motion is detected by PIR2 (reading equals HIGH), the presence of a visitor is confirmed.
  - The visitor count is incremented (`visitors++`), `lastRIPdetected` is reset to 0, and "Visitor entered. Visitors: [visitor count]" is printed to the serial interface.

This summarizes how the code functions in detail and how it tracks visitor count using PIR motion sensors.
