# Adafruit SHT45 Room Climate for Tessera

> Beta hardware-plugin prototype for the Guition ESP32-S3-4848S040 (4-inch, 480 × 480), without relays.

## P1 wiring (UART0 repurposed as I²C)

| P1 header | ESP32-S3 | SHT45 |
|---|---:|---|
| GND | GND | GND |
| RXD | GPIO44 | SDA |
| TXD | GPIO43 | SCL |
| 5V | 5V | VIN |

I²C address: `0x44`. Update interval: 5 seconds. The Adafruit SHT45 breakout is designed to accept VIN supply and includes I²C level shifting; verify the board markings and VIN range before powering it.

**UART0 caveat:** GPIO43/44 are the ESP32-S3 UART0 pins. Reusing them for I²C may disable or disrupt serial logs, UART communication, and USB-UART flashing/debugging on this board. USB native-CDC flashing may still work depending on board wiring and bootloader configuration, but this must be tested on the actual hardware. If UART0 is needed, use the alternate GPIO40/GPIO2 configuration instead.

## Alternative wiring

`plugin-gpio40-gpio2.yaml` is the fallback configuration for the expansion header:
- GPIO40 = SDA
- GPIO2 = SCL
- 5V = VIN
- GND = GND

Only one of these I²C configurations should be active.

## Sensor entities

- `SHT45 Raumtemperatur`
- `SHT45 Luftfeuchtigkeit`

Tessera can display the resulting Home Assistant entities using its existing sensor/value tiles. This initial package does not implement a custom-drawn Tessera tile.

## Test procedure

1. Back up Home Assistant and the current Tessera configuration.
2. Confirm P1 labels and wiring on the physical board before connecting.
3. Install only if the actual Tessera plugin loader accepts this package format and the selected screen is the Guition 4-inch model.
4. Build and flash.
5. Inspect ESPHome logs / I²C scan. The sensor should respond at `0x44`.
6. Confirm both sensor entities update at 5-second intervals.
7. Test serial logging and future firmware flashing before considering this configuration permanent.

## Compatibility status

This is an experimental configuration package, not a verified Tessera build. It has not been compiled against the user's Tessera installation or tested on physical hardware. The plugin manifest/API version fields are provisional and must be checked against the exact Tessera plugin SDK/manifest specification before installation.
