# News Ticker — STM32 + ESP32 + AWS IoT

This project aims to make a live news ticker that fetches real-time headlines from the internet and scrolls them across a display The device pulls live information from the internet and presents it in real time, using a low-cost microcontroller.

---

## Implementation

The system uses two microcontrollers working together:

- **STM32 Nucleo-F401RE** — the main application processor. It handles the display, parses incoming data, and drives the scrolling ticker logic.
- **ESP32-WROOM-32** — acts as a Wi-Fi modem. The STM32 sends it standard AT commands over UART, and the ESP32 handles all Wi-Fi and HTTP communication transparently.

The STM32 sends an HTTP GET request (via AT commands through the ESP32) to a news API, receives the response, extracts the headlines, and renders them as a scrolling ticker on the display. All firmware on the STM32 side was written in C using the STM32 HAL library.

**Key implementation details:**
- UART4 used for STM32 ↔ ESP32 communication
- AT command sequencing handled with a custom state machine
- JSON response parsed on the STM32 with lightweight string processing
- Display driven over SPI/I2C with a custom scrolling routine

---

## Key feattures

- How to use a secondary MCU (ESP32) as a network co-processor via AT commands — a common pattern in cost-constrained IoT products
- Designing a reliable UART communication layer between two microcontrollers, including handling timing, buffering, and error recovery
- Parsing structured text (JSON) in a memory-constrained environment without dynamic allocation
- End-to-end thinking across hardware, firmware, and cloud — from wiring a circuit to consuming a live web API on a microcontroller

---

## Stack

`C` · `STM32 HAL` · `UART / AT Commands` · `ESP32` · `HTTP` · `AWS IoT` · `STM32CubeIDE`

---

## Hardware

| Board | Role |
|---|---|
| STM32 Nucleo-F446RE | Main MCU |
| ESP32-WROOM-32 DevKit | Wi-Fi co-processor |

