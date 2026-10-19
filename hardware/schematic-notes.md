# DipTrace schematic implementation notes — Rev A

## Sheets
1. Controller: U1 ESP32-S3-WROOM-1U-N8, EN and GPIO0 reset/boot, status LED, native USB data with ESD and USB-C CC resistors.
2. Thermocouple acquisition: U2–U9 MAX31856, each with Type K differential input, locally decoupled supplies, recommended input filter and independent CS; common SPI bus.
3. Storage/debug: U10 W25Q128 data NOR (independent CS), programming/debug points and internal temperature measurement provision.
4. Power: USB-derived regulated 3.3 V bench supply. Battery and power-path circuit deliberately TBD pending thermal testing.

## Required design reviews before routing
- Check U1 module pad numbering, supply pins, USB pinout, strap pin constraints and peak Wi-Fi current.
- Check U2–U9 datasheet pins: SPI SCK/SDI/SDO/CS, thermocouple T+/T-, AVDD/DVDD/AGND/DGND and any unused alarm pins.
- Use actual Analog Devices recommended analog input filter and grounding rather than relying on conceptual diagrams.
- Cold-junction accuracy: place thermocouple alloy-to-copper transitions near the CJC sensing region; avoid gradients caused by radio and regulators. A remote harness transition can invalidate the chip's CJC.
- Verify SPI flash voltage, command set, JEDEC ID, capacity, erase endurance and write completion behavior. Buffer records safely; store monotonic sequence numbers, timestamps, CRC and profile session ID.
- Verify USB-C connector orientation and pin duplication, USB ESD, USB series resistor recommendation and power backfeed prevention.
- Test that a 3.3 V LDO supplies peak radio current at the chosen 5V input and worst-case internal temperature.
- Include independent internal enclosure temperature measurement and an out-of-range fault indication.
- Consider thermocouple open/short detection, input protection, common-mode noise and grounded-junction thermocouple compatibility.
- Keep battery charging strictly outside the oven; battery selection and thermal cutoff TBD.
- Set current and final dimensional/mechanical clearance limits only after real conveyor measurements and barrier tests.

**No production-ready netlist or electrical rule check exists yet.**
