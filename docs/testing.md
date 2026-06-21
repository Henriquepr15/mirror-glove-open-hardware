# Mirror Glove Testing Procedure

This document describes the basic testing procedure used to validate the Mirror Glove open hardware prototype.

## 1. Purpose

The testing procedure verifies whether the Mirror Glove prototype can acquire coherent signals from five flexible resistive sensors positioned on a wearable glove.

The tests evaluate:

- Electrical continuity.
- Sensor response.
- Analog reading stability.
- Effect of the RC low-pass filter.
- Individual finger response.
- Gesture recording.
- Optional actuator response.

## 2. Electrical inspection

Before powering the circuit:

1. Visually inspect all solder joints.
2. Check the orientation and placement of connectors.
3. Use a multimeter to verify that there is no short circuit between power and ground.
4. Verify continuity between each sensor connector and the corresponding analog input.
5. Inspect loose wires or unstable connections.

## 3. Power-on test

1. Connect the ESP32-C6 Super Mini to the computer using a USB cable.
2. Open the serial monitor or data acquisition interface.
3. Confirm that the firmware starts correctly.
4. Verify whether five sensor channels are displayed.
5. Confirm that no channel is fixed, saturated, disconnected, or showing abnormal noise.

## 4. Individual sensor test

Test each finger sensor separately:

1. Keep the glove still.
2. Move only one finger.
3. Observe whether the expected channel changes.
4. Return the finger to the relaxed position.
5. Repeat the process for all five fingers.

Suggested mapping:

- Thumb
- Index finger
- Middle finger
- Ring finger
- Pinky finger

## 5. Static stability test

With the glove at rest:

1. Keep the hand still for a short period.
2. Record the raw ADC readings.
3. Observe whether the values remain stable.
4. Compare filtered and unfiltered readings when available.

This test helps evaluate whether the RC low-pass filter reduces fast fluctuations and signal instability.

## 6. Gesture test

Perform simple gestures and verify whether the sensor readings change coherently:

- Open hand.
- Closed hand.
- Pointing gesture.
- Pinch gesture.
- OK gesture.
- Thumbs-up gesture.

Each gesture should produce a different combination of sensor readings.

## 7. Dataset recording test

To validate data collection:

1. Define the gesture label before recording.
2. Record a sequence of samples.
3. Save the timestamp, gesture label, and five sensor readings.
4. Repeat the process for all target gestures.
5. Inspect the dataset for missing values, mislabeled samples, or unstable channels.

## 8. Optional receiver and actuator test

If the receiver board and servomotors are used:

1. Upload the receiver firmware to the second ESP32 board.
2. Confirm that the receiver obtains the transmitted sensor data.
3. Connect the servomotors.
4. Map each sensor value to the corresponding actuator.
5. Move each finger and observe whether the corresponding servo responds proportionally.

## 9. Known limitations

The current prototype is intended for experimental validation. The tests verify signal acquisition and preliminary gesture differentiation, but they do not validate clinical use, long-term durability, anatomical accuracy, or medical safety.

Further tests are required to evaluate:

- Long-term sensor stability.
- Repeated wearing and repositioning of the glove.
- Inter-user variability.
- Mechanical durability.
- Wireless communication reliability.
- Actuator response under load.
