# Mirror Glove Calibration Procedure

This document describes the basic calibration procedure for the Mirror Glove flexible sensor readings.

## 1. Purpose

The calibration procedure is used to relate the raw analog-to-digital converter readings from each flexible sensor to the approximate motion range of each finger. Since each sensor may present different electrical and mechanical behavior, calibration is required before data collection or actuator control experiments.

## 2. Required setup

Before calibration, make sure that:

- The five flexible sensors are connected to the PCB.
- The ESP32 firmware is uploaded.
- The serial monitor or data acquisition interface is open.
- The five sensor channels are being displayed correctly.
- The glove is positioned on the user’s hand in a stable and repeatable way.

## 3. Minimum and maximum readings

For each finger, record two approximate reference values:

- `ADC_min`: value measured when the finger is in the relaxed or extended position.
- `ADC_max`: value measured when the finger is flexed within the intended range of motion.

This process must be repeated for:

- Thumb
- Index finger
- Middle finger
- Ring finger
- Pinky finger

## 4. Normalization

The sensor reading can be normalized using the following equation:

`normalized_value = (ADC_current - ADC_min) / (ADC_max - ADC_min)`

Where:

- `ADC_current` is the current raw reading.
- `ADC_min` is the minimum reference value.
- `ADC_max` is the maximum reference value.

The normalized value can be used to compare sensors with different raw ranges or to map finger flexion to actuator commands.

## 5. Servo mapping

When the hardware is used for motion mirroring experiments, the normalized value can be mapped to a servomotor angle:

`servo_angle = angle_min + normalized_value * (angle_max - angle_min)`

Where:

- `angle_min` is the minimum allowed servo angle.
- `angle_max` is the maximum allowed servo angle.

The limits must be selected carefully to avoid mechanical stress on the actuator or experimental prosthetic mechanism.

## 6. Calibration recommendations

- Calibrate the glove after wearing it, not before.
- Avoid excessive finger force during calibration.
- Repeat calibration if the glove position changes.
- Repeat calibration if a sensor is removed or repositioned.
- Inspect unstable readings before collecting data.
- Avoid using saturated ADC values as calibration limits.

## 7. Limitations

This calibration procedure provides an approximate proportional representation of finger flexion. It does not directly measure anatomical joint angles and should not be interpreted as a clinical measurement without further validation.
