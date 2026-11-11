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

Sensors are shown in the main device **"Guiton 4 Inch"**:
- `sensor.guiton4inch_room_temperature` - Temperature in °C
- `sensor.guiton4inch_humidity` - Humidity in %

Tessera can display sensors with a **Sensor/Value Tile**. The hardware interface is defined by the plugin; create the visual tile in the Tessera Layout Editor.

## Test procedure

1. Connect the wiring as shown above before powering the screen.
2. In Tessera, open **Plugins**, enable **Adafruit SHT45 Room Climate**, and select your Guition 4-inch screen.
3. Build and flash. Watch the ESPHome logs in the build output for:
   - `I2C scan found device at address 0x44`
   - Sensor updates at 5-second intervals
4. In Home Assistant, verify temperature and humidity sensors appear under the **Guiton 4 Inch** device, updating every 5 seconds.

## Version History

### 0.1.2
- Removed `device_info` block (not supported in ESPHome 2026.x)
- Updated documentation to reflect that sensors appear under main device "Guiton 4 Inch"

### 0.1.1
- Initial release with I²C SHT4x sensor integration

