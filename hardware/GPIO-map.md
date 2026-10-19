# Proposed GPIO allocation — Rev A

**Tentative, not yet pinout/ERC verified.** Use the exact ESP32-S3-WROOM-1U-N8 module datasheet and Espressif hardware design guidelines before PCB layout.

| ESP32-S3 signal | Function |
|---|---|
| GPIO12 | SPI SCK |
| GPIO11 | SPI MOSI -> MAX31856 SDI and storage DI |
| GPIO13 | SPI MISO <- MAX31856 SDO and storage DO |
| GPIO4-10 | TC1–TC7 CS (one per channel) |
| GPIO14 | TC8 CS |
| GPIO15 | external data flash CS |
| GPIO19 | native USB D- |
| GPIO20 | native USB D+ |
| GPIO16 | status LED |
| GPIO17 | reserved battery monitoring (ADC suitability to verify) |
| GPIO18 | reserved internal temperature measurement |
| GPIO0 | BOOT strap switch |
| EN | Reset switch and pull-up |

All SPI clients share clock/data; each requires a separate inactive-high chip select. Configure bus speeds and transaction modes per client. Include test points. Ensure no internal flash/PSRAM reserved pins or boot-strap requirements are violated.

Use USB-C CC1 and CC2 each with a 5.1k Rd resistor to ground for the USB device role; follow Espressif USB and ESD guidance.
