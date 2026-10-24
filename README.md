# ESP32-S3 Micromouse Robot Controller

A custom 2-layer PCB designed in KiCad for an autonomous maze-solving Micromouse robot. The board handles power regulation, motor driver signals, and distance sensors using an ESP32-S3 microcontroller.

<p align="center">
  <img src="Media/board_3d.png" alt="Micromouse 3D Model" width="550">
</p>

## Overview

This board acts as the main compute and interface hub for a Micromouse robot. It steps down 5V USB power to a clean 3.3V rail for the MCU, routes dual I2C channels to front-facing distance sensors, and breaks out control lines to drive dual DC motors through an external H-bridge.

## Hardware Features

* Microcontroller: ESP32-S3-WROOM-1 module with native USB (D+/D-) on GPIO 19 and 20 for direct programming and debugging.
* Power: USB Type-C connector with 5.1k pull-downs on CC lines for standard 5V negotiation, stepped down through an AMS1117-3.3 regulator.
* Sensor Headers: Dedicated 4-pin headers (J3 and J4) for left and right I2C distance sensors, with onboard 4.7k pull-up resistors on SCL and SDA lines.
* Motor Driver Header: 6-pin interface (J2) breaking out 5V, GND, two PWM speed signals, and two direction signals for dual H-bridge motor drivers.
* Programming and Controls: Tactile switches for Reset and Boot mode selection with debounce and pull-up circuitry.
* Mounting: Four M2.5 corner mounting holes positioned for robot chassis assembly.

## Board Layout and Design Verification

<p align="center">
  <img src="Media/board_layout.png" alt="KiCad PCB Layout" width="550">
</p>

* Layer stackup: 2-layer FR4, 1.6 mm thickness, 1 oz copper.
* Ground planes: Top and bottom layers flooded with ground copper pours tied with thermal reliefs.
* RF Keep-Out: The ESP32-S3 PCB antenna hangs off the top edge of the board with all copper and traces pulled back to prevent RF attenuation.
* Verification: Passed KiCad DRC with 0 errors, 0 unconnected nets, and 0 schematic parity warnings.

## Schematic

The circuit is organized into three sub-blocks: USB-C power entry and LDO regulation, ESP32-S3 core control circuitry, and the sensor/actuator header interfaces.

[View Full Schematic PDF](Media/esp32_micromouse_schematic.pdf)

<p align="center">
  <img src="Media/schematic.png" alt="Schematic" width="700">
</p>

## Key Components

| Ref | Part | Package | Description |
| :--- | :--- | :--- | :--- |
| U1 | AMS1117-3.3 | SOT-223 | 5V to 3.3V LDO regulator |
| U2 | ESP32-S3-WROOM-1 | SMD Module | Main processor |
| J1 | USB-C 16-pin | SMD | 5V power input and USB data |
| J2 | 1x06 Pin Header | 2.54 mm TH | Dual H-bridge motor driver interface |
| J3, J4 | 1x04 Pin Header | 2.54 mm TH | Left and right I2C distance sensor headers |
| SW1, SW2 | Tactile Switch | 6x6 mm | Reset and Boot buttons |
| R1, R2 | 5.1k Resistor | 0805 | USB-C CC termination |
| R3, R4 | 10k Resistor | 0805 | EN and Boot pull-ups |
| R5, R6 | 4.7k Resistor | 0805 | I2C pull-ups |
| C1, C2 | 10uF Capacitor | 0805 | LDO input and output decoupling |
| C3, C4 | 0.1uF / 1uF Capacitor | 0805 | Power filtering and reset debounce |

## Repository Structure

* Hardware_Files: KiCad project file (.kicad_pro), schematic (.kicad_sch), and PCB layout (.kicad_pcb).
* Gerbers_Micromouse_v1.0.zip: Production gerbers and drill files ready for PCB manufacturing.
* 3D Models: Component 3D step and wrl files.
* Media: Screenshots, renders, and schematic PDF for documentation.

## Author

Julio Tito  
Rutgers University – New Brunswick  
Electrical and Computer Engineering
