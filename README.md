# STM32 Low Voltage Telemetry & Control System

This repository contains the firmware and simulation implementations for the three STM32 technical milestones assigned by the ASU Racing Team Low Voltage sub-team[cite: 1]. Each milestone is structured as an independent STM32CubeIDE project with corresponding simulation files[cite: 1].

---

## Repository Structure

* `Milestone_1/` – STM32CubeIDE project for GPIO verification[cite: 1]
* `Milestone_2/` – STM32CubeIDE project for dual ADC monitoring via UART[cite: 1]
* `Milestone_3/`
  * `Master/` – SPI Master controller with UART command interface[cite: 1]
  * `Slave/` – SPI Slave telemetry sensor node[cite: 1]
* `Simulation/` – Proteus schematic designs (`.pdsprj`) and compiled binary/hex files[cite: 1]

---

## Milestone Overviews

### Milestone 1: Toolchain Validation & LED Blinking
* **Objective:** Verify the development workflow, HAL library integration, and basic clock configurations by toggling an on-board LED[cite: 1].
* **Implementation:** Configured GPIO pin `PC13` as a push-pull output[cite: 1]. The pin toggles state periodically inside the main execution loop with a 500 ms delay using `HAL_GPIO_TogglePin()` and `HAL_Delay()`[cite: 1].

### Milestone 2: Analog Telemetry Acquisition via ADC & UART
* **Objective:** Sample multi-channel analog sensor inputs and stream formatted telemetry metrics over serial communication[cite: 1].
* **Implementation:** Configured `ADC1` to sample two independent analog channels (`PA0` and `PA1`) mapped to potentiometers modeling Engine Temperature and Throttle Position[cite: 1]. Channels are sampled sequentially in regular conversion mode[cite: 1], scaled to engineering units (°C, %)[cite: 1], formatted into string buffers, and transmitted to a Virtual Terminal via `USART1`[cite: 1].

### Milestone 3: Master-Slave SPI Telemetry Network
* **Objective:** Implement a distributed master-slave communication architecture simulating an automotive sensor network[cite: 1].
* **Implementation:** 
  * The Master node interfaces with a serial Virtual Terminal over `USART1` to accept user-entered Case IDs[cite: 1].
  * The Master forwards the request ID to the Slave over `SPI1` using software-controlled chip select (`PB0` $\rightarrow$ Slave `PA4`)[cite: 1].
  * The Slave node decodes the ID and responds with a packed 24-bit struct containing defined Voltage Level and Wheel Speed data[cite: 1].
  * The Master receives the payload, extracts the fields, and outputs the decoded parameters to the terminal[cite: 1].

---

## Hardware & Simulation Notes (Milestone 3)

* **MCU Target Selection:** The project requirements originally referenced the `STM32F103C8T6`[cite: 1]; however, this implementation was built using the **`STM32F103C6` (specifically `STM32F103C6T6`)** to maintain full compatibility with the Proteus Blue Pill simulation model shown in the schematic capture.
* **First-Input Behavior:** During simulation, the very first entered Case ID returns a garbage value due to initial shift-register preloading and SPI pipeline priming between the master and slave. After this first transaction cycle, the SPI frames synchronize properly, and every subsequent input works cleanly and displays the expected telemetry data.

---

## Software & Toolchain Requirements

* **IDE:** STM32CubeIDE V1.19[cite: 1]
* **HAL Driver:** STM32F1xx HAL Driver Package[cite: 1]
* **Simulation:** Proteus 8 Professional with STM32 VSM library support[cite: 1]
