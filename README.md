# Adafruit SHT45 Room Climate for Tessera

> Hardware plugin for the Guition ESP32-S3-4848S040 (4-inch, 480 × 480), without relays.

## Expansion header wiring (GPIO40/GPIO2)

| Header pin | ESP32-S3 | SHT45   |
|-----------:|---------:|---------|
| GND        | GND      | GND     |
| GPIO40     | SDA      | SDA     |
| GPIO2      | SCL      | SCL     |
| 5V         | 5V       | VIN     |

I²C address: `0x44`. Update interval: 5 seconds. The Adafruit SHT45 breakout is designed to accept VIN supply and includes I²C level shifting; verify the board markings and VIN range before powering it.

**Note:** GPIO2 is shared with status LEDs on some Guition boards. If you see unexpected LED behavior, try the alternative UART0 pins (GPIO43/44) instead.

## Sensor entities

- `sensor.sht45_raumklima_temperatur`
- `sensor.sht45_raumklima_feuchtigkeit`

Tessera can display the resulting Home Assistant entities using its existing sensor/value tiles. This plugin defines the hardware interface; you create the visual tile in Tessera's Layout editor.

## Device info

Both sensors appear under a single Home Assistant device:

- **Device name:** SHT45 Raumklima  
- **Manufacturer:** Adafruit  
- **Model:** SHT45 Precision Humidity and Temperature Sensor  

This makes it easier to group, rename, or automate all room-climate sensors together.

## Test procedure

1. Connect the wiring as shown above before powering the screen.
2. In Tessera, open **Plugins**, enable **Adafruit SHT45 Room Climate**, and select your Guition 4-inch screen.
3. Build and flash. Watch the ESPHome logs in the build output for:
   - `I2C scan found device at address 0x44`
   - Sensor updates at 5-second intervals
4. In Home Assistant, verify a new device **SHT45 Raumklima** appears with temperature and humidity entities updating every 5 seconds.

## Compatibility status

Production-ready plugin for Tessera + ESPHome. Tested on Guition ESP32-S3-4848S040 with Adafruit SHT45 breakout at I²C address `0x44`.
