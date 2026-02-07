# Ferris Shield for ZMK

Custom Ferris keyboard configuration as a shield for nice!nano v2.

## Building

```bash
west build -b nice_nano_v2 -- -DSHIELD=ferris
```

## Flashing

1. Double-tap reset button on nice!nano v2
2. Drag and drop `build/zephyr/zmk.uf2` to the USB drive

## Hardware

- Controller: nice!nano v2
- Left side: Direct GPIO connection
- Right side: MCP23017 I2C GPIO expander

## Pin Configuration

Update the GPIO pins in `ferris.overlay` to match your actual wiring.

Left side uses nice!nano pro_micro pins:
- Columns: D1, D0, D2, D3, D4  
- Rows: D7, D8, D9, D10

Right side uses MCP23017 GPIOs 3-7 (cols) and 8-11 (rows).

I2C is on the default nice!nano I2C pins (pro_micro_i2c).
