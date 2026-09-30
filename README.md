# Gesture-Controlled Mecanum Wheel Car

Two ESP32 boards communicate over ESP-NOW: an MPU6050-based handheld transmitter sends tilt data to a four-motor mecanum-wheel receiver.

## Provenance and licence

- Original source: [un0038998/Gesture_Controlled_Mecanum_Wheel_Car](https://github.com/un0038998/Gesture_Controlled_Mecanum_Wheel_Car)
- Reviewed upstream revision: [`3e83829`](https://github.com/un0038998/Gesture_Controlled_Mecanum_Wheel_Car/tree/3e83829559ff84d40057f0666ed6ab992fabde6c)
- Original author and copyright holder: Ujwal Nandanwar
- Licence: MIT; see [LICENSE](LICENSE)

This repository preserves the upstream attribution. A device-specific ESP-NOW peer address was replaced with a zero placeholder; set it to the receiver ESP32's address before use.

## Supported boards

- Two ESP32 development boards supported by the Arduino ESP32 core

## Parts list

- 2 × ESP32 development boards
- 1 × MPU6050 accelerometer/gyroscope module
- 4 × DC geared motors with mecanum wheels
- Motor drivers capable of independently driving four DC motors
- Robot chassis, suitable battery supply, wiring and power regulation

Check motor-driver current limits and use a shared ground. Do not power motors directly from an ESP32 board.

## Required libraries

- Arduino ESP32 core (`WiFi.h`, `esp_now.h`)
- Arduino `Wire` library
- I2Cdevlib `I2Cdev` and `MPU6050_6Axis_MotionApps20`

## Pin allocation

### Receiver motor-driver connections

| Motor | IN1 | IN2 | Enable / PWM |
| --- | ---: | ---: | ---: |
| Back right | GPIO 16 | GPIO 17 | GPIO 22 |
| Back left | GPIO 18 | GPIO 19 | GPIO 23 |
| Front right | GPIO 26 | GPIO 27 | GPIO 14 |
| Front left | GPIO 33 | GPIO 25 | GPIO 32 |

The transmitter uses the selected ESP32 board's default I2C pins for the MPU6050. Verify those pins against the board documentation before wiring.

## Sketches

- `GetMacAddress/GetMacAddress.ino`: prints an ESP32 station MAC address.
- `Car_Transmitter/Car_Transmitter.ino`: reads the MPU6050 and sends motion data.
- `Car_Receiver_Simple_Movement/Car_Receiver_Simple_Movement.ino`: receives data and drives four motors.

## Schematic status

The staged source does not contain a machine-readable schematic. The upstream repository contains diagram images, but their electrical correctness has not been independently verified. Review the upstream diagrams and confirm pin assignments, voltage levels, grounding and motor power before building.

## Review status

Source, provenance and licence were checked for publication. Hardware operation has not been independently reproduced by OpenMakerProjects.

- Compilation: **Passed** for the receiver, transmitter and MAC-address sketches using Arduino CLI and Arduino ESP32 core 2.0.18-arduino.5. I2Cdevlib was used for the transmitter build.
- Secret scan: **Passed**; the upstream device-specific peer MAC address was replaced by a zero placeholder.
- Binary and duplicate scan: **Passed**; no compiled files, installers, archives or duplicate files are included.
- Hardware test: **Not tested**.
