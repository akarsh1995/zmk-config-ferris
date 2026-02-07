# Akeeb Shield for ZMK

Single-controller keyboard with MCP23017 I/O expander for right half.

## Hardware

- **1× nice!nano v2** controller (mounted on left half)
- **1× MCP23017** I2C GPIO expander (mounted on right half, address 0x20)
- **I2C cable** connecting left and right halves (4 wires: SDA, SCL, VCC, GND)
- Akeeb keyboard (34 keys: 4 rows × 10 columns)

## Architecture

This is a **unified keyboard** with one controller using composite kscan:
- **Left half**: 4 rows + 5 columns wired directly to nice!nano GPIO
- **Right half**: 4 rows + 5 columns wired to MCP23017 GPIO via I2C cable
- Each half is scanned independently, then combined by ZMK

## Building

GitHub Actions builds automatically. Or build locally:

```bash
west build -b nice_nano_v2 -- -DSHIELD=akeeb
```

## Flashing

1. Double-tap reset on nice!nano v2 (on left half)
2. Drag `build/zephyr/zmk.uf2` to USB drive that appears
3. Only left half needs flashing (right half is passive)

## Pin Configuration

### nice!nano GPIO (Left Half)
**Rows**: pro_micro pins 6, 7, 8, 9  
**Columns**: pro_micro pins 21, 20, 19, 18, 15

### MCP23017 GPIO (Right Half)
**Rows**: GPIO pins 8, 9, 10, 11  
**Columns**: GPIO pins 3, 4, 5, 6, 7

### I2C Connection
Connect left and right halves with 4-wire cable:
- nice!nano Pin 2 (P0.17/SDA) → MCP23017 Pin 13 (SDA)
- nice!nano Pin 3 (P0.20/SCL) → MCP23017 Pin 12 (SCL)
- VCC → VCC (3.3V)
- GND → GND

**MCP23017 I2C Address:** 0x20  
**Clock Speed:** 400kHz (I2C_BITRATE_FAST)

## Wiring Summary

1. **Left half wiring**: Connect row and column switches to nice!nano GPIO
   - Rows → pins 6, 7, 8, 9
   - Columns → pins 21, 20, 19, 18, 15

2. **Right half wiring**: Connect row and column switches to MCP23017 GPIO
   - Rows → GPIO 8, 9, 10, 11
   - Columns → GPIO 3, 4, 5, 6, 7

3. **I2C cable**: 4-wire cable between nice!nano (pins 2/3 + power) and MCP23017 (SDA/SCL + power)

Update pin assignments in `akeeb.overlay` to match your actual PCB wiring.

