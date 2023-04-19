# Troublesome chips:

Some sensors or chips have non-standard behavior that causes issues when
trying to use I2C. Here's a few of the ones to watch for

- AGS20MA - Use a bus speed of 20-30 kHz.
- ATECCx08 - Use slow-speed I2C to get out of sleep mode.
- BNO055, BNO085 - Uses clock stretching, violates I2C protocol timing in some caes, and sometimes needs to be reset. Does not work well on i.MX RT10xx chips, ESP32, ESP32-S3.
- CCS811 - Uses clock stretching.
- LC709203F - Repeated start, clock stretching, sleep mode
- MCP9600 (date codes 1845 or before) - bug: duplicate data from register.
  reads, perhaps due to clock stretching.
- MCP9600, MCP9601 - Repeated start, clock stretching. Often will not
  respond to zero-length writes, so scanning the I2C bus to find the
  device can fail.
- PN532 - Clock stretching.

If you're using Raspberry Pi with these chips, check out our
[guide on how to work-around clock stretching](https://learn.adafruit.com/circuitpython-on-raspberrypi-linux/i2c-clock-stretching).

# Troublesome microcontrollers:

- MicroChip Atmel SAMD21, SAMx5x - I2C bus frequency below 95 kHz not available when I2Cperipheral is drive with a 48 MHz clock,
  which is typical. CircuitPython checks for out-of-range bus frequencies.
