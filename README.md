# ZMK Config for Akeeb Keyboard

Custom ZMK firmware configuration for the Akeeb keyboard using nice!nano v2.

## ✅ Correct Structure (Shield-based)

```
boards/shields/akeeb/
├── akeeb.overlay         # Hardware configuration
├── akeeb.keymap          # Keymap layout  
├── akeeb.conf            # Build config options
├── Kconfig.shield         # Shield declaration
├── Kconfig.defconfig      # Default configs
├── akeeb.zmk.yml         # Metadata
└── README.md
```

## Building

```bash
west build -b nice_nano_v2 -- -DSHIELD=akeeb
```

Or let GitHub Actions build it automatically when you push.

## Flashing

1. Double-tap reset button on nice!nano v2
2. Drag `build/zephyr/zmk.uf2` to the USB drive that appears

## Customization

- **Keymap**: Edit `boards/shields/akeeb/akeeb.keymap`
- **Hardware pins**: Edit `boards/shields/akeeb/akeeb.overlay`
- **Build options**: Edit `boards/shields/akeeb/akeeb.conf`

## Hardware Requirements

- nice!nano v2 (or compatible Pro Micro nRF52840 board)
- MCP23017 I2C GPIO expander for right half
- Akeeb keyboard PCB

## Important Notes

⚠️ **The old `boards/pierrechevalier83/ferris/` directory is now obsolete** and should be removed. The shield-based approach in `boards/shields/akeeb/` is the correct structure for ZMK user config repositories.

## Pin Configuration

Update the GPIO pins in `akeeb.overlay` to match your actual wiring. See the shield README for details.
