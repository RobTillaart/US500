
[![Arduino CI](https://github.com/RobTillaart/US500/workflows/Arduino%20CI/badge.svg)](https://github.com/marketplace/actions/arduino_ci)
[![Arduino-lint](https://github.com/RobTillaart/US500/actions/workflows/arduino-lint.yml/badge.svg)](https://github.com/RobTillaart/US500/actions/workflows/arduino-lint.yml)
[![JSON check](https://github.com/RobTillaart/US500/actions/workflows/jsoncheck.yml/badge.svg)](https://github.com/RobTillaart/US500/actions/workflows/jsoncheck.yml)
[![GitHub issues](https://img.shields.io/github/issues/RobTillaart/US500.svg)](https://github.com/RobTillaart/US500/issues)

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/RobTillaart/US500/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/RobTillaart/US500.svg?maxAge=3600)](https://github.com/RobTillaart/US500/releases)
[![PlatformIO Registry](https://badges.registry.platformio.org/packages/robtillaart/library/US500.svg)](https://registry.platformio.org/libraries/robtillaart/US500)


# US500

Arduino library for US500 underwater distance sensor.

## Description

**Experimental**

This library is to use the US500 underwater distance sensor.
The sensor communicates over Serial at 9600 baud.
The MCU sends a command and depending on the command the device answers.

The device can read a distance up to 50 centimetre (20 inch) and read the temperature.
Furthermore it has a start and stop function. These functions are straight forward.

The library is not tested with hardware (order pending).

Feedback, as always is welcome.


### Warnings from datasheet

1. Please make sure the Ultrasonic sensor probe unite perpendicular to the object( around 90°±5°)
When the ultrasonic sensor measure the object. If the angle bigger than 90°±5°,the signal will lose.
2. Please keep the sensor probe fixed for the test and do not hold it with your hand.That would affect
the signal.
3. The controller is not waterproof. Please do not submerge the controller in water.
4. This sensor is calibrated based on underwater measurement scenarios.
Cannot be use in air measurement scenarios.


### Related

- https://www.positive-inno.com - supplier of the US500 (and other sensors).
- https://github.com/RobTillaart/US500 - this library
- https://github.com/RobTillaart/SRF05 - library for SRF05 distance sensor with temperature and humidity compensation.
- https://www.tinytronics.nl/nl/sensoren/afstand/pono-us500-hx-onderwater-ultrasone-afstandssensor-uart-50cm


### Tested

TODO


## Interface

```cpp
#include "US500.h"
```

### Constructor

- **US500(Stream \* str)** Typical Serial1 or Serial2.
It is not known if software serial will work (not tested).

### Core

If the functions return a value < 0, it is an error code.

- **float getDistance()** returns the distance in cm (or error code).
- **int setMaxDistance(uint16_t distance)** set the maximum range in 0.1 mm
Must be between 1500 and 5000.
returns 0 = false or 1 = true (or error code).
- **float getTemperature()** returns the temperature in degrees Celsius.
(or error code).
The resolution is in steps of 0.1 degree, supports negative values.
- **void startMeasurement()** idem.
- **void stopMeasurement()** idem.


### Error codes

|  name                 |  value  |
|:----------------------|:-------:|
|  US500_CMD_ERROR      |    -1   |
|  US500_CRC_ERROR      |    -2   |
|  US500_TIMEOUT_ERROR  |    -3   |


### Helper

- **void flush()** if communication is out of sync, 
one can flush int input buffer.


## Future

#### Must

- improve documentation
- get hardware
- test, test, test

#### Should

- improve error handling
- add range check for setMaxDistance or constrain.
- verify software serial works / not.
- test temperature range (water is typical > 0).
- do we need to compensate distance for temperature?
  or is this done in the factory.
- time for measurement after start
- performance indication. per function.

#### Could

- create unit tests if possible

#### Wont


## Support

If you appreciate my libraries, you can support the development and maintenance.
Improve the quality of the libraries by providing issues and Pull Requests, or
donate through PayPal or GitHub sponsors.

Thank you,


