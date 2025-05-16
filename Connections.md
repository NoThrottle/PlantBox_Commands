# Arduino Connection Guide

This document provides a guide for connecting components to the Arduino board for the project.

## Adafruit 16-Channel PWM & Servo Driver (PCA9685)

- **I2C Communication**
  - `SCL` -> Connect to Arduino `A5` (Analog Pin 5)
  - `SDA` -> Connect to Arduino `A4` (Analog Pin 4)
- **Power**
  - `VCC` -> Connect to Arduino `5V`
  - `GND` -> Connect to Arduino `GND`
- **External Power (Optional)**
  - `V+` -> Connect to external power source for servos (ensure voltage matches servo requirements).

## PN532 NFC Module

- **SPI Communication**
  - `MOSI` -> Connect to Arduino `D11`
  - `MISO` -> Connect to Arduino `D12`
  - `SCK` -> Connect to Arduino `D13`
  - `SS` (Chip Select) -> Connect to Arduino `D10`
- **Power**
  - `VCC` -> Connect to Arduino `5V`
  - `GND` -> Connect to Arduino `GND`

## SPI Devices (e.g., Adafruit SPI Registers)

- **SPI Communication**
  - `MOSI` -> Connect to Arduino `D11`
  - `MISO` -> Connect to Arduino `D12`
  - `SCK` -> Connect to Arduino `D13`
  - `CS` -> Connect to a digital pin (e.g., `D10` or any available pin).
- **Power**
  - `VCC` -> Connect to Arduino `5V`
  - `GND` -> Connect to Arduino `GND`

## RGB LED

- **Connections**
  - `R` -> Connect to a PWM pin (e.g., `D3`)
  - `G` -> Connect to a PWM pin (e.g., `D5`)
  - `B` -> Connect to a PWM pin (e.g., `D6`)
  - `GND` -> Connect to Arduino `GND`

## Soil Moisture Sensor

- **Connections**
  - `VCC` -> Connect to Arduino `5V`
  - `GND` -> Connect to Arduino `GND`
  - `Signal` -> Connect to an analog pin (e.g., `A0`)

## Pump

- **Connections**
  - `VCC` -> Connect to external power source (ensure voltage matches pump requirements).
  - `GND` -> Connect to Arduino `GND`
  - `Control` -> Connect to a digital pin (e.g., `D9` via a transistor or relay).

# Arduino Connections for PlantBox

This document outlines the connections and pin assignments for the PlantBox project.

## Pin Assignments

### PWM Channels

- **Red**: PWM Channel `0`
- **Green**: PWM Channel `1`
- **Blue**: PWM Channel `2`
- **Pump**: PWM Channel `3`

### Digital Pins

- **Buzzer**: Pin `8`
- **PN532_SS** (NFC Module): Pin `10`

### Analog Pins

- **Soil Sensor**: Analog Pin `A0`
- **Reservoir Sensor**: Analog Pin `A1`

## Additional Notes

- The PWM channels are managed using the `Adafruit_PWMServoDriver` library.
- The NFC module uses the `PN532_SPI` interface with the `PN532_SS` pin for chip select.
- Ensure all components are properly connected and powered to avoid damage to the Arduino or peripherals.

## Notes

- Ensure all components share a common ground (`GND`).
- Use appropriate resistors, capacitors, or level shifters if required by the components.
- Double-check voltage levels to avoid damaging components or the Arduino board.
