# Akeeb Shield for ZMK

Akeeb keyboard configuration using nice!nano v2 with MCP23017 I/O expander.

## Hardware

- **1x nice!nano v2** controller
- **1x MCP23017** I2C GPIO expander (address 0x20)
- Akeeb keyboard (34 keys: 4 rows × 10 columns)
- **Left 5 columns**: Direct to nice!nano GPIO
- **Right 5 columns**: Via MCP23017 expander

## Building

```bash
west build -b nice_nano_v2 -- -DSHIELD=akeeb
```

Or let GitHub Actions build automatically.

## Flashing

1. Double-tap reset button on nice!nano v2
2. Drag `zmk.uf2` to the USB drive

## Pin Configuration

Update GPIO pins in `akeeb.overlay` to match your wiring:

### Left Half (Direct to nice!nano)
**Rows**: D7, D8, D9, D10  
**Columns**: D1, D0, D2, D3, D4

### Right Half (MCP23017)
**Columns**: GPIO 7, 6, 5, 4, 3 (GPA7-GPA3)

### I2C Connection
- **SDA**: Default I2C pin on nice!nano
- **SCL**: Default I2C pin on nice!nano  
- **MCP23017 Address**: 0x20

Adjust pins in the overlay to match your actual PCB layout.

I2C is on the default nice!nano I2C pins (pro_micro_i2c).
