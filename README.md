# Dactyl CT70

# CT70 ZMK Configuration

A 7x5 split keyboard configuration for ZMK firmware, inspired by the Kinesis Advantage 360 layout.

## Features
- 7 columns × 5 rows per side (70 keys total)
- Kinesis Advantage 360 inspired layout
- Homerow shift modifiers on F and J keys
- 4 layers: Default, Function, Keypad, Space
- Nice!Nano v2 controller support
- GitHub Actions automated firmware building

## Hardware Requirements
- 2x Nice!Nano v2 controllers
- Split keyboard PCB with 7x5 matrix
- Pin connections as specified in overlay files

## Installation
1. Fork this repository
2. Enable GitHub Actions
3. Push changes to trigger build
4. Download firmware from Actions artifacts
5. Flash ct70_left.uf2 to left controller
6. Flash ct70_right.uf2 to right controller

## Pin Mapping
- Rows: D3(GPIO1), D4(GPIO0), D5(GPIO2), D6(GPIO3), D7(GPIO4)
- Columns: See overlay files for specific GPIO assignments

## Layer Layout
- Layer 0: QWERTY with Kinesis-style positioning
- Layer 1: Function keys (F1-F10)
- Layer 2: Numpad and Bluetooth controls
- Layer 3: Space layer for thumb access