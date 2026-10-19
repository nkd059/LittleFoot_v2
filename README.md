# Little Foot ZMK configuration

This configuration targets a single Little Foot rev2.3 fitted with a nice!nano v2. It uses the QMK source's `LAYOUT_big_space_base`: 5 matrix rows, 10 columns, with its single bottom-row spacebar switch at matrix row 4, column 5.

## Hardware details used

The QMK board files specify `COL2ROW` diodes and these Pro Micro / ATmega32U4 matrix pins:

- Rows: F6, B6, B2, B3, B1
- Columns: F5, F7, B5, B4, E6, D7, C6, D4, D0, D1

The shield overlay translates those same Pro Micro footprint pads to nice!nano v2 nRF52840 GPIOs. Rows use pull-downs, matching the working Hammer40 ZMK matrix scan pattern. The repo's firmware describes 17 WS2812 RGB LEDs on F4; this initial ZMK config doesn't enable that effect. The QMK source declares no encoder or display.

## Build

The included `build.yaml` is ready for the ZMK GitHub Actions build workflow. From a ZMK west workspace with this repository checked out as `config`, the equivalent local target is:

```sh
west build -s zmk/app -b nice_nano//zmk -- -DSHIELD=littlefoot
```

The resulting UF2 is normally at `build/zephyr/zmk.uf2`. Put the nice!nano into its bootloader by double-tapping reset, then copy that UF2 to the `NICENANO` USB drive. The board reboots when flashing finishes.

The default layer is QWERTY with a hold layer on the rightmost home-row key and a shift spacebar, adapted from the supplied QMK `LAYOUT_big_space_base`. Lower and Raise provide navigation, function, and symbol keys. QMK tap dances, combos, and custom text macros are not included in this basic ZMK keymap.
