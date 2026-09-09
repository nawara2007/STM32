# STM32 Low Voltage Telemetry & Control System

This repository contains the firmware and simulation implementations for the three STM32 technical milestones assigned by the ASU Racing Team Low Voltage sub-team. Each milestone is structured as an independent STM32CubeIDE project with corresponding simulation files.
---

## Hardware & Simulation Notes (Milestone 3)

* **MCU Target Selection:** The project requirements originally referenced the `STM32F103C8T6`[cite: 1]; however, this implementation was built using the **`STM32F103C6` (specifically `STM32F103C6T6`)** to maintain full compatibility with the Proteus Blue Pill simulation model shown in the schematic capture.
* 
* **First-Input Behavior:** During simulation, the very first entered Case ID returns a garbage value due to initial shift-register preloading and SPI pipeline priming between the master and slave. After this first transaction cycle, the SPI frames synchronize properly, and every subsequent input works cleanly and displays the expected telemetry data.

---

## Software & Toolchain Requirements

* **IDE:** STM32CubeIDE V1.19[cite: 1]
* **HAL Driver:** STM32F1xx HAL Driver Package[cite: 1]
* **Simulation:** Proteus 8 Professional with STM32 VSM library support, and BluePill Library[cite: 1]
