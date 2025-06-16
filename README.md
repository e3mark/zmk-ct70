# Dactyl CT70

## https://claude.ai/ AI Prompt

Please update this codebase https://github.com/e3mark/zmk-ct70 to name the keyboard as ct70, also update the matrix to 7columns by 5 rows with default_layer similar keymaps to kinesis 360. Use the pins D3 to d7 for rows, and D21 down to D15 for columns.

# CT70 ZMK Configuration

A 7×5 split keyboard configuration for ZMK firmware, inspired by the Kinesis Advantage 360 layout.

## Features

- **70 keys total**: 7 columns × 5 rows per side
- **Kinesis Advantage 360 inspired layout**: Familiar key positioning for Kinesis users
- **4 layers**: Default QWERTY, Function, Numpad, and Bluetooth
- **Nice!Nano v2 support**: Optimized for wireless split keyboards
- **GitHub Actions**: Automated firmware building

## Hardware Requirements

- 2x Nice!Nano v2 controllers
- Split keyboard PCB with 7×5 matrix
- Pin connections as specified in overlay files

## Pin Configuration

### Rows (D3-D7)
- Row 0: D3 (GPIO1)
- Row 1: D4 (GPIO0) 
- Row 2: D5 (GPIO2)
- Row 3: D6 (GPIO3)
- Row 4: D7 (GPIO4)

### Columns (D21 down to D16)
- Column 0: D21
- Column 1: D20
- Column 2: D19
- Column 3: D18
- Column 4: D17 (D10 equivalent)
- Column 5: D16
- Column 6: D15 (for 7th column)

## Getting Started

1. **Fork this repository**
2. **Enable GitHub Actions** in your forked repository
3. **Push changes** to trigger the build process
4. **Download firmware** from the Actions artifacts
5. **Flash firmware**:
   - Flash `ct70_left.uf2` to the left controller
   - Flash `ct70_right.uf2` to the right controller

## Layout

### Default Layer (QWERTY)
```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐     ┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ ESC │  1  │  2  │  3  │  4  │  5  │  =  │     │  -  │  6  │  7  │  8  │  9  │  0  │BKSP │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┤     ├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│ TAB │  Q  │  W  │  E  │  R  │  T  │  [  │     │  ]  │  Y  │  U  │  I  │  O  │  P  │  \  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┤     ├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│CAPS │  A  │  S  │  D  │  F  │  G  │  `  │     │  '  │  H  │  J  │  K  │  L  │  ;  │ENTER│
├─────┼─────┼─────┼─────┼─────┼─────┼─────┤     ├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│LSHFT│  Z  │  X  │  C  │  V  │  B  │HOME │     │ END │  N  │  M  │  ,  │  .  │  /  │RSHFT│
└─────┴─────┴─────┼─────┼─────┼─────┼─────┤     ├─────┼─────┼─────┼─────┼─────┴─────┴─────┘
                  │LCTRL│LALT │ SPC │ FN  │     │ FN  │ SPC │RALT │RCTRL│
                  └─────┴─────┴─────┴─────┘     └─────┴─────┴─────┴─────┘
```

### Function Layer
- **F1-F12**: Function keys across top row
- **Arrow keys**: WASD on left side, arrow cluster on right side
- **Page Up/Down**: Accessible via thumb keys
- **Delete**: Replaces backspace

### Numpad Layer
- **Bluetooth controls**: BT1-BT5 and clear on left side
- **Number pad**: Full numpad layout on right side
- **Mathematical operators**: +, -, *, /, =

### Bluetooth Layer
- **Device switching**: Quick access to paired devices
- **Bluetooth clear**: Reset all connections

## File Structure

```
ct70-zmk/
├── .github/
│   └── workflows/
│       └── build.yml          # GitHub Actions workflow
├── config/
│   ├── west.yml              # West configuration
│   ├── ct70.keymap           # Main keymap file
│   ├── ct70.dtsi             # Device tree include
│   ├── ct70_left.overlay     # Left side pin configuration
│   ├── ct70_right.overlay    # Right side pin configuration
│   ├── Kconfig.defconfig     # Default configuration
│   └── Kconfig.shield        # Shield configuration
└── README.md
```

## Customization

### Modifying the Keymap

Edit `config/ct70.keymap` to customize key bindings. The keymap uses standard ZMK keycodes and behaviors.

### Changing Pin Assignments

Modify the GPIO assignments in:
- `config/ct70_left.overlay` - Left side pins
- `config/ct70_right.overlay` - Right side pins

### Adding Layers

Add new layers to the keymap by:
1. Adding a new layer definition in `ct70.keymap`
2. Creating layer toggle/momentary keys to access the new layer

## Development Workflow

### Local Development
```bash
# Initialize west workspace
west init -l config
west update
west zephyr-export

# Build left side
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=ct70_left

# Build right side  
west build --pristine -s zmk/app -b nice_nano_v2 -- -DSHIELD=ct70_right
```

### Quick Iteration
After making changes to the keymap:
```bash
# Clean and rebuild (if needed)
west build -d build/left -b nice_nano_v2 -- -DSHIELD=ct70_left --pristine
west build -d build/right -b nice_nano_v2 -- -DSHIELD=ct70_right --pristine
```

## Features

### Split Keyboard Support
- **Central/Peripheral**: Left side acts as central, right as peripheral
- **Wireless**: Full Bluetooth Low Energy support
- **Battery monitoring**: Built-in battery level reporting

### Layer Management
- **Momentary layers**: Hold key to activate layer
- **Toggle layers**: Tap to switch between layers
- **Transparent keys**: Fall through to lower layers

### Bluetooth Features
- **5 device profiles**: Switch between multiple paired devices
- **Connection management**: Clear and re-pair devices as needed
- **Low power**: Optimized for battery life

## Troubleshooting

### Build Issues
- Ensure all files are properly formatted
- Check GPIO pin assignments match your hardware
- Verify ZMK dependencies are up to date

### Connectivity Issues
- Reset Bluetooth on both halves
- Clear all pairings and re-pair
- Check battery levels on both controllers

### Key Issues
- Verify matrix configuration matches physical layout
- Check diode direction in hardware
- Test individual switches with multimeter

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This configuration is released under the MIT License. See the individual files for specific copyright information.

## Acknowledgments

- **ZMK Firmware**: The amazing keyboard firmware that makes this possible
- **Kinesis**: Inspiration for the ergonomic layout
- **Community**: Thanks to all the contributors and testers
   

