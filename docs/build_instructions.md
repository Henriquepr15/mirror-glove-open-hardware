# Mirror Glove Build Instructions

This document describes the basic assembly procedure for the Mirror Glove open hardware prototype. The system consists of a wearable glove with five flexible resistive sensors, a custom PCB, signal conditioning components, an ESP32-C6 Super Mini microcontroller, firmware for data acquisition, and optional receiver-side actuator control.

## 1. Required materials

The main materials required to build the Mirror Glove prototype are:

* 1 fabric glove
* 5 flexible resistive sensors
* 1 custom Mirror Glove PCB
* 1 ESP32-C6 Super Mini module
* 5 fixed resistors for voltage dividers
* Capacitors for passive RC low-pass filtering
* Sensor connectors
* Pin headers or board connectors
* Jumper wires or flexible wires
* USB cable
* Computer with Arduino IDE or PlatformIO
* Soldering iron and solder wire
* Multimeter
* Optional: receiver ESP32 board and servomotors for motion mirroring experiments

A complete bill of materials is provided in `bom/bill_of_materials.csv`.

## 2. Sensor positioning on the glove

Place one flexible resistive sensor on each finger of the glove. The sensors should be aligned with the natural flexion axis of the fingers.

Suggested mapping:

* Sensor 1: thumb
* Sensor 2: index finger
* Sensor 3: middle finger
* Sensor 4: ring finger
* Sensor 5: pinky finger

Each sensor should be positioned longitudinally on the dorsal side of the glove so that finger flexion causes mechanical bending of the sensor.

## 3. Sensor wiring

Each flexible sensor is connected as part of a voltage divider circuit. The voltage divider converts the resistance variation of the flexible sensor into an analog voltage that can be read by the ESP32 analog-to-digital converter.

General connection:

* One terminal of the flexible sensor is connected to the supply/reference side of the voltage divider.
* The other terminal is connected to the analog reading node.
* A fixed resistor is connected between the analog reading node and the reference/ground side, according to the selected circuit configuration.
* The analog reading node is connected to one ESP32 analog input.

Repeat this circuit for all five sensors.

## 4. Signal conditioning

A passive RC low-pass filter is used to reduce fast fluctuations and noise in the analog readings. A capacitor is connected between the analog reading node and GND.

The RC filter is intended to attenuate fast oscillations caused by electrical noise, unstable contact, mechanical vibration, and touch-related interference, while preserving the slower signal variations associated with finger flexion.

## 5. PCB assembly

Solder the components onto the Mirror Glove PCB according to the schematic and board layout files provided in the `hardware/` directory.

Recommended assembly order:

1. Solder passive SMD components such as resistors and capacitors.
2. Solder connectors for the flexible sensors.
3. Solder pin headers or connectors for the ESP32-C6 Super Mini module.
4. Inspect all solder joints visually.
5. Use a multimeter to check for short circuits between power and ground.
6. Connect the ESP32-C6 Super Mini to the PCB.
7. Connect the five flexible sensors to the corresponding sensor inputs.

## 6. Firmware upload

Upload the transmitter firmware to the ESP32-C6 Super Mini using Arduino IDE or PlatformIO.

The firmware should perform the following functions:

* Read the five analog sensor channels.
* Associate each sensor value with its corresponding finger.
* Send readings to the serial monitor or store/transmit the data.
* Optionally transmit the values to a receiver board for motion mirroring.

Firmware files are provided in the `firmware/` directory.

## 7. Initial power-on test

Before wearing the glove, perform a basic power-on test:

1. Connect the ESP32 board to the computer through USB.
2. Open the serial monitor.
3. Check whether five sensor readings are being displayed.
4. Move each sensor manually and verify whether the corresponding reading changes.
5. Confirm that no channel is fixed, saturated, disconnected, or unstable.

## 8. Glove integration

After validating each sensor channel individually, attach the sensors permanently or semi-permanently to the glove. The attachment method should allow the sensor to bend naturally with the finger while avoiding excessive mechanical stress at the sensor terminals.

Recommended practices:

* Avoid sharp bends near the sensor terminals.
* Use flexible wires when possible.
* Provide strain relief near connection points.
* Keep sensor cables organized to avoid pulling during finger movement.

## 9. Calibration before use

Before collecting data, calibrate each sensor by recording approximate minimum and maximum ADC values for each finger.

The calibration procedure is described in `docs/calibration.md`.

## 10. Functional test

After assembly and calibration, perform the following functional test:

1. Wear the glove.
2. Open the serial monitor or data acquisition interface.
3. Move each finger individually.
4. Verify whether the expected sensor channel responds.
5. Perform simple gestures such as open hand, closed hand, pointing, pinch, OK gesture, and thumbs-up.
6. Record a short dataset and inspect whether the readings are coherent.

Testing procedures are described in `docs/testing.md`.

## 11. Notes and limitations

This prototype is intended for experimental data acquisition and research in wearable interfaces, assistive technology, gesture analysis, and prosthetics-related studies. It is not a medical device and should not be used for clinical decision-making without further validation, ethical approval, and regulatory assessment.
