# ULTRA-LOW-POWER-SMART-LOGGER using ESP32
## HARDWARE DESIGN
### Objective:
To create a smart logger that can:
•Run for over 3 months on one Li-ion battery.
•Use deep sleep modes to consume minimal power.
•Only wake up on sensor triggers or scheduled intervals..
System Architecture Overview
### Main Components:

ESP32-WROOM-Main controller (Wi-Fi, sleep modes)
DHT22-Temperature and humidity sensor
MQ-2-Gas leakage detection
TP4056-Battery charging and protection
MCP1700-3302E-LDO regulator to supply stable 3.3V
Li-ion Battery-Power source
UART header-Debugging and programming interface
USB-C Port-Charging the battery via TP4056
## PCB Design (KiCad)
### Key Highlights:
•Custom 2-layer PCB designed in KiCad v9.
•Copper ground fill used to improve stability and reduce EMI.
•Minimal trace length and proper decoupling capacitors used to avoid noise.
•All pins clearly marked for easier debugging.
•Placement optimized to allow a compact but accessible layout.
### Power Flow:
•USB-C VBUS → TP4056 (U2) → Battery → MCP1700 (U3) → 3.3V net
•3.3V net powers DHT22, MQ2, ESP32
•GND common across all components
### Gerber Output:
•All necessary layers: F.Cu, B.Cu, F.Silk, F.Mask, Edge.Cuts, Drill file etc. exported and verified.
•DRC run and fixed for clearance, hole size, unconnected pads.
•Footprints assigned for all parts from Digi-Key KiCad libraries.
## FIRMWARE (WOKWI SIMULATION)
Features Implemented:
•Sleep Mode: ESP32 spends most of the time in deep sleep.
•Interrupt-based wake-up using GPIO (e.g., MQ-2 trigger).
•Timed Wake-up: RTC timer used to wake up ESP32 every few hours.
•Temperature Logging: DHT22 readings logged only if temp > threshold.
•MQ-2 Gas Sensor: When gas concentration crosses the limit, ESP wakes up and stores event.
Smart Logic:
•Device intelligently decides when to store logs to conserve memory.
•Debounce and hysteresis logic implemented to avoid false triggers
•Device intelligently decides when to store logs to conserve memory.
•Debounce and hysteresis logic implemented to avoid false triggers
