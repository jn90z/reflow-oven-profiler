# Wireless Reflow Oven Profiler

ESP32-S3-based, eight-channel Type K wireless/recording profiler for the **Heller 1809 MK7**. Designed to ride alongside an instrumented PCB on an interchangeable edge-rail or mesh-belt carrier.

**Status: Rev A architecture and BOM only. Not yet thermally or electrically validated. Do not run an active prototype through an oven.**

## Design files
- [Starter BOM](hardware/BOM-revA.csv)
- [GPIO allocations](hardware/GPIO-map.md)
- [DipTrace schematic notes](hardware/schematic-notes.md)
- [Architecture and data packet](docs/architecture.md)
- [Enclosure and conveyor carriers](mechanical/carriers-and-barrier.md)
- [Firmware plan](firmware/README.md)
- [Windows GUI and prediction plan](software/README.md)

## Goals
Capture eight thermocouples at 2–5 Hz/channel. Write every frame to onboard nonvolatile storage. Stream frames over Wi-Fi when available, and automatically recover missing samples after oven exit. Analyze real profiles and eventually predict changes to Heller 1809 MK7 upper/lower zones and conveyor speed.

## First steps
1. Verify datasheets, part numbers, library symbols and footprints before creating the DipTrace schematic.
2. Bench-test MAX31856 cold-junction accuracy with ESP32 Wi-Fi transmission.
3. Implement stored sequence-numbered records and the Windows receiver.
4. Validate a passive thermal barrier with an internal dummy load; separately validate conveyor clearance and RF performance before adding electronics or batteries.

No DipTrace schematic/PCB files, validated thermal shield or working firmware are included yet.
