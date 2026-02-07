# ZMK Config for Akeeb Keyboard

Custom ZMK firmware configuration for the Akeeb keyboard using nice!nano v2.

## ✅ Correct Structure (Shield-based)

```
boards/shields/akeeb/
├── akeeb.overlay         # Hardware configuration (unified)
├── akeeb.keymap          # Keymap layout  
├── akeeb.conf            # Build config (I2C enabled)
├── Kconfig.shield        # Shield declaration
├── Kconfig.defconfig     # Default configs
├── akeeb.zmk.yml         # Metadata
└── README.md
```

## Building

```bash
west build -b nice_nano_v2 -- -DSHIELD=akeeb
```

Or let GitHub Actions build it automatically when you push.

## Flashing

1. Double-tap reset button on nice!nano v2 (on left half)
2. Drag `build/zephyr/zmk.uf2` to the USB drive that appears
3. Only the left half needs firmware (right half is passive with MCP23017)

## Customization

- **Keymap**: Edit `boards/shields/akeeb/akeeb.keymap`
- **Hardware pins**: Edit `boards/shields/akeeb/akeeb.overlay`
- **Build options**: Edit `boards/shields/akeeb/akeeb.conf`

## Hardware Requirements

- 1× nice!nano v2 (or compatible Pro Micro nRF52840 board) - mounted on left half
- 1× MCP23017 I2C GPIO expander - mounted on right half
- I2C cable connecting left and right halves (SDA/SCL + power/ground)
- Akeeb keyboard PCB

## Important Notes

⚠️ **The old `boards/pierrechevalier83/ferris/` directory is now obsolete** and should be removed. The shield-based approach in `boards/shields/akeeb/` is the correct structure for ZMK user config repositories.

**Architecture**: Uses composite kscan - left half has its own 4×5 matrix on nice!nano GPIO, right half has its own 4×5 matrix on MCP23017 GPIO. Each half is scanned independently.

## Pin Configuration

Update the GPIO pins in `akeeb.overlay` to match your actual wiring:
- **Left half**: 4 rows + 5 columns on nice!nano GPIO (pins 6-9 for rows, 21/20/19/18/15 for columns)
- **Right half**: 4 rows + 5 columns on MCP23017 GPIO (GPIO 8-11 for rows, GPIO 3-7 for columns)
- **I2C connection**: nice!nano pins 2 (SDA/P0.17) and 3 (SCL/P0.20)

See the shield README for detailed pin mappings and I2C configuration.


## Pin Configuration

Update the GPIO pins in `akeeb.overlay` to match your actual wiring. See the shield README for details.
