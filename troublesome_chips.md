<!--- SPDX-FileCopyrightText: 2022 Alec Delaney for Adafruit Industries --->
<!--- SPDX-License-Identifier: MIT --->

# Troublesome chips:

Some sensors or chips have non-standard behavior that causes issues when
trying to use I2C. Here's a few of the ones to watch for

- BNO055 - Clock stretching, and sometimes needs to be reset
- ATECCx08 - Use slow-speed I2C to get out of sleep mode
- MCP9600 (date codes 1845 or before) - bug: duplicate data from register
  reads, perhaps due to clock stretching
- MCP9600, MCP9601 - Repeated start, clock stretching. Often will not
  respond to zero-length writes, so scanning the I2C bus to find the
  device can fail.
- PN532 - Clock stretching
- CCS811 - Clock stretching
- LC709203F - Repeated start, clock stretching, sleep mode

If you're using Raspberry Pi with these chips, check out our
[guide on how to work-around clock stretching](https://learn.adafruit.com/circuitpython-on-raspberrypi-linux/i2c-clock-stretching).
