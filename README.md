# ESPHome RS232 Controller for Dell 1609WX Projector

This project was created to integrate the only remaining non-automated component of my home theater setup into Home Assistant: a Dell 1609WX projector.

While it would have been possible to control the projector using infrared (IR), I decided to use the RS232 serial interface instead. The main reason is reliability and two-way communication. Unlike IR, serial communication allows the controller not only to send commands, but also to receive status information directly from the projector.

The project is based on:

* ESP32-C6
* ESPHome
* Home Assistant
* RS232 communication using a MAX3232 interface

## Why RS232 Instead of IR?

Infrared control is simple and common in home theater environments, but it has several limitations:

* One-way communication only
* No device feedback
* Requires line-of-sight
* Less reliable in some installations

Using RS232 enables:

* Two-way communication
* Real projector status reporting
* Reliable command delivery
* Better automation possibilities
* Potential diagnostic and monitoring features

This makes the integration much more robust and interesting from a Home Assistant perspective.

## A Different Approach for Home Assistant

Most projector integrations in Home Assistant rely on:

* Infrared blasters
* HDMI-CEC
* Network APIs (when available)

This project explores something less common in DIY smart home environments:
direct RS232 serial integration using ESPHome.

The idea is to create a flexible serial bridge that can:

* receive commands from Home Assistant
* communicate directly with legacy AV equipment
* report device states back into the automation system

Many older professional and semi-professional AV devices still expose RS232 ports, even when they lack modern network control.

## Future Possibilities

Although this project is currently focused on the Dell 1609WX projector, the hardware architecture is intentionally generic.

In theory, with different firmware or ESPHome configurations, this same hardware platform could be adapted to control virtually any RS232-compatible equipment, including:

* projectors
* AV receivers
* matrix switchers
* amplifiers
* industrial equipment
* lighting controllers
* legacy automation systems

The board was designed to be simple, compact, and reusable.

## Current Project Status

⚠️ This project is still in active development.

The hardware design, PCB layout, and firmware are evolving and may change significantly over time.

Current development areas include:

* ESPHome serial handling
* two-way communication parsing
* Home Assistant entity integration
* command reliability
* power handling
* debugging and diagnostics

## Open Source and Contributions

If you are interested in:

* ESPHome
* Home Assistant
* serial communication
* retro/legacy hardware integration
* RS232 automation
* PCB design

your help, ideas, testing, and contributions are very welcome.

Feel free to:

* open issues
* suggest improvements
* fork the project
* contribute code or hardware ideas

## Technologies Used

* ESPHome
  https://esphome.io/

* Home Assistant
  https://www.home-assistant.io/

## Repository Contents

This repository will include:

* KiCad PCB files
* schematic files
* ESPHome YAML files
* photos
* development notes
* future firmware revisions

The goal is to document the entire process from concept to a fully integrated smart home RS232 controller.
