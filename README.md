# Galia
Modular split ergonomic keyboard system with each half consisting of a central motherboard and a hot-swappable key cluster daughterboard to allow for maximum flexibility.

## Disclaimer
This keyboard is licensed under [CERN-OHL-S-2.0](https://cern-ohl.web.cern.ch/) and is compatible with both [QMK Firmware](https://qmk.fm/) and [ZMK Firmware](https://zmk.dev).

## Key Features
### Motherboard
* Fully reversible, compact (38.0x70.9mm), and designed to fit onto the top inner corner of a split keyboard.
* On-board STM32G0B1CCU7 processor.
* ESD-protected USB-C input port and USB-C split comms ports with ideal diode configuration for reverse current protection on VBUS input.
* Connects to daughterboard through fully ESD-protected 2.54mm pitch 02x08 pogo receptacle header in [VIK](https://github.com/sadekbaroudi/vik) breakout layout with three additional GPIO.
* 4-layer (signal/ground/power/signal) PCB, guard ring, and star ground connection point in between USB port shields to reduce EMI.
* 5V output rail limited to ~188mA through the use of a TPS2553 current limiting switch with EN pin controlled through firmware to reduce RGB LED quiescent current draw.
* 2.54mm SWD and TC2030-NL [Paw-Connect](https://github.com/LeoDJ/Paw-Connect) header for debugging purposes.
* 9 extra IO available on a 2.54mm-pitch header aligned to the same grid as the pogo header.
* On-board button[Acheron](https://acheronproject.com/reset_article_1/reset_article_1/#52-substituting-the-jfet) single-button reset circuit.
### Daughterboard (TBC)
* Connects to motherboard through fully ESD-protected 2.54mm pitch 02x08 pogo pin header.
* Matrix scan planned to be implemented through 74HC595 SIPO shift registers for low power draw and compatibility with ZMK interrupt functionality.
* Also compatible with charlieplex, duplex, and standard matrix layouts.
* WS2812 and AP102 RGB LED support.
* Additional [VIK](https://github.com/sadekbaroudi/vik) header support if desired.
* Reset pin connected to pogo pin header to allow for relocation of reset button on daughterboard.

## Pogo header pinout
| Function/description                 | Pin name | Row 1 | Row 2 | Pin name | Function/description                  |
| ------------------------------------ | -------- | ----- | ----- | -------- | ------------------------------------- |
| Active high, hold for 3s for DFU     | N/A      | RST   | GPIO5 | A1       | SPI2 SCK/TIM1 CH2/ADC IN1             |
| USART2 TX/TIM2 CH3/ADC IN2           | A2       | GPIO4 | GPIO3 | A3       | SPI2 MISO/USART2 RX/TIM15 CH2/ACD IN3 |
| 200mA max draw across system         | N/A      | 3V3   | GND   | N/A      | N/A                                   |
| I2C2 SDA                             | B14      | SDA   | SCL   | B13      | I2C2 SCL                              |
| SPI2 MOSI/TIM2 CH4                   | B11      | RGB   | 5V    | N/A      | 188mA max draw by daughterboard       |
| USART3 TX/SPI2 MISO/ACD IN10         | B2       | GPIO1 | MOSI  | A7       | SPI1 MOSI                             |
| USART3 RX/TIM3 CH3/TIM1 CH2N/ADC IN8 | B0       | GPIO2 | CS    | A4       | SPI1 NSS                              |
| SPI1 MISO                            | A6       | MISO  | SCK   | A5       | SPI1 SCK                              |

## VIK keyboard certification card
| Category                 | Classification          | Response           |
| -----------------------  | ----------------------- | ------------------ |
| FPC connector            | Required                | 2.54mm pogo header |
| Breakout pins            | Recommended             | :heavy_check_mark: |
| Supplies: SPI            | Strongly recommended    | :heavy_check_mark: |
| Supplies: I2C            | Strongly recommended    | :heavy_check_mark: |
| I2C on main PCB          | Discouraged             | No                 |
| I2C pull ups             | Informative             | No                 |
| Supplies: RGB            | Strongly recommended    | :heavy_check_mark: |
| Supplies: Extra GPIO 1   | Required                | Analog/Digital     |
| Supplies: Extra GPIO 2   | Required                | Analog/Digital     |

## Changelog
* 2026/09/16: V0.1 motherboard initial commit.