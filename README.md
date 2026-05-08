# ESPHome RS232 Controller

An open-source ESPHome and Home Assistant compatible RS232 controller based on the ESP32-C6 platform.

---

# Hardware Preview

## 3D PCB Side View

![PCB Side View](Hardware/V1.0/PCB%203D%20side%20V1.0.png)
---

## PCB Layout

![PCB Layout](Hardware/V1.0/PCB%20layout%20V1.0.png)

---

# Project Overview

This project started from a simple goal: integrate the only remaining non-automated device in my home theater setup into Home Assistant, a Dell 1609WX projector.

Instead of using traditional infrared (IR) control, I decided to use the projector's native RS232 serial interface to enable reliable two-way communication and deeper integration capabilities.

---

# Why RS232 Instead of IR?

Most DIY home theater integrations use:

* infrared blasters
* HDMI-CEC
* Wi-Fi APIs
* network-based integrations

While IR would have worked for this projector, it comes with important limitations:

* one-way communication only
* no feedback from the device
* line-of-sight dependency
* limited reliability
* no real status monitoring

Using RS232 changes everything.

With serial communication, the controller can:

* send commands to the projector
* receive responses from the projector
* monitor status information
* improve reliability
* support advanced automations
* potentially detect errors or states

This makes the integration much more robust and significantly more interesting from a Home Assistant perspective.

---

# A Different Kind of ESPHome Project

ESPHome is typically used for:

* sensors
* relays
* lights
* switches
* environmental monitoring

This project explores a less common use case:
using ESPHome as a bidirectional RS232 bridge for legacy AV equipment.

The idea is to create a flexible serial controller capable of:

* communicating with older professional equipment
* integrating legacy hardware into modern smart homes
* exposing serial devices inside Home Assistant
* translating serial protocols into automation entities

Many older devices still include RS232 ports even when they lack:

* Wi-Fi
* Ethernet
* APIs
* smart integrations

This project attempts to bridge that gap.

---

# Hardware Platform

The controller is based on:

* ESP32-C6
* ESPHome
* MAX3232 RS232 transceiver
* custom KiCad PCB

The hardware includes:

* RS232 communication
* two-way serial support
* ESD protection
* power filtering
* debug UART header
* I2C expansion header
* compact form factor

The design currently uses a:

* Seeed Studio XIAO ESP32-C6

for simplicity, USB programming convenience, and modularity.

---

# Firmware Development Status

⚠️ IMPORTANT: The firmware is still experimental and has not yet been fully validated.

At the current stage, the hardware appears to be functioning correctly, and the ESP32-C6 is already receiving UART data from the projector successfully.

Current debug logs confirm:

* UART communication is active
* the MAX3232 interface is working
* TX/RX wiring appears correct
* the projector is responding
* the selected baud rate (19200) is correct
* the Dell serial protocol is active

The project has already passed one of the most critical phases:
establishing stable bidirectional serial communication with the projector.

Current development is focused on:

* reverse engineering the Dell protocol
* packet parsing
* CRC validation
* ACK/NACK handling
* source tracking
* power state synchronization
* lamp hour reporting
* Home Assistant media_player integration

At the moment, the firmware is capable of detecting UART packets, but the protocol parser is still under active development and has not yet been fully tested or validated.

Example debug output currently looks like:

```text
[D][projector:051]: UART packet received
```

The next firmware steps involve logging the actual hexadecimal payloads to fully decode the projector protocol structure.

Once packet decoding is complete, the goal is to implement:

* real-time projector state tracking
* synchronized Home Assistant status
* reliable command acknowledgment
* professional-grade RS232 integration

Interestingly, the projector appears to transmit packets approximately every second, suggesting:

* heartbeat packets
* periodic status responses
* active query replies

This is an excellent sign and indicates that full two-way integration is likely achievable.

---

# Future Possibilities

Although this project currently targets the Dell 1609WX projector, the hardware architecture was intentionally designed to be generic and reusable.

With different firmware or ESPHome configurations, this same board could theoretically control almost any RS232-compatible equipment, including:

* projectors
* AV receivers
* matrix switchers
* amplifiers
* lighting systems
* industrial equipment
* automation processors
* legacy control systems

The long-term idea is to create a reusable ESPHome RS232 platform that can integrate older serial devices into modern smart home ecosystems.

---

# Current Project Status

⚠️ IMPORTANT: This project is still in active development.

The hardware and firmware are currently considered experimental and may change significantly over time.

Current development areas include:

* ESPHome UART handling
* serial protocol parsing
* two-way communication reliability
* Home Assistant entity mapping
* debugging and diagnostics
* power management refinements
* support for additional RS232 devices

At this stage:

* the PCB is functional
* hardware validation is ongoing
* firmware development is still evolving

---

# Open Source Contributions

If you are interested in:

* ESPHome
* Home Assistant
* embedded systems
* serial communication
* legacy hardware integration
* PCB design
* RS232 automation

your help is very welcome.

Contributions, ideas, testing, pull requests, and suggestions are greatly appreciated.

Feel free to:

* open issues
* suggest improvements
* fork the project
* contribute firmware
* improve hardware
* test with other RS232 devices

---

# Technologies Used

## ESPHome

https://esphome.io/

ESPHome provides the firmware framework and Home Assistant integration layer used by this project.

---

## Home Assistant

https://www.home-assistant.io/

Home Assistant is used as the main automation platform and user interface.

---

# Repository Contents

This repository includes:

* KiCad project files
* schematics
* PCB layouts
* ESPHome YAML files
* hardware previews
* development notes
* future firmware revisions

The goal is to document the entire development process from concept to a fully integrated smart-home-compatible RS232 controller.

---

# Project Goals

* Integrate legacy RS232 equipment into Home Assistant
* Explore two-way serial communication with ESPHome
* Create a reusable RS232 ESPHome platform
* Share hardware and firmware openly
* Learn and experiment with embedded automation systems

---

# License

This project is currently being developed as an open-source hobby and learning platform.
