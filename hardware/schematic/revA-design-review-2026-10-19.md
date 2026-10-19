# Rev A detailed schematic and BOM work package (2026-10-19)

The detailed BOM (112 line items including deliberate TBDs), pin-net checklist (334 connections), and four-page PDF schematic reference were generated as conversation download attachments.

**These attachments are not yet committed as binary/CSV files to this repository.** The earlier `hardware/BOM-revA.csv` is a preliminary BOM and does not supersede the new detailed downloadable CSV.

## Critical corrections to earlier concept
- MAX31856 pinout TSSOP-14: 1 AGND, 2 BIAS, 3 T-, 4 T+, 5 AVDD, 6 DNC, 7 DRDY, 8 DVDD, 9 CS, 10 SCK, 11 SDO, 12 SDI, 13 FAULT, 14 DGND.
- Per Analog Devices input filter: two 100-ohm series input resistors; 100 nF **across** filtered T+/T-; two 10 nF common-mode capacitors to ground; BIAS connected to filtered T-.
- ESP32-S3-WROOM-1U-N8 module physical pads: 2 +3V3; 1,40,41 GND; 3 EN; 27 GPIO0; 20 GPIO12 SPI_SCK; 19 GPIO11 SPI_MOSI; 21 GPIO13 SPI_MISO; 13 GPIO19 USB_D-; 14 GPIO20 USB_D+.
- U11 AP2112K-3.3TRG1: 1 VIN, 2 GND, 3 EN, 4 NC, 5 VOUT. Bench power only; verify 600 mA peak capacity and thermal load.
- USB J1 Adam Tech USB-C31-S-RA-EH2.0B-BK-T/R. **Exact pad placement/cutout requires Adam Tech drawing**; USB-C A/B contacts do not imply footprint pad ordering.
- The provisional Wurth 691137710002 TC terminals are **not Type-K-compensated connectors**. CJC error remains unresolved.
- No battery power path or independent internal barrier-temperature safety circuit is complete; no in-oven prototype use yet.

## Source datasheets
- https://documentation.espressif.com/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf
- https://www.analog.com/media/en/technical-documentation/data-sheets/MAX31856.pdf
- https://www.analog.com/en/products/max31856.html

## Review gates
Resolve cold-junction transition, physical connector footprint, flash SPI details, RF antenna thermal rating, 3.3V power capacity, battery system and thermal enclosure before manufacturing release. Run DipTrace ERC/DRC after placing real symbols and footprints.
