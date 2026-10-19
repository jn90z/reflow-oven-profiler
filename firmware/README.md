# Firmware roadmap (ESP-IDF / C++)

1. Board bring-up, GPIO and USB logging.
2. MAX31856 SPI driver, fault register polling, 8-channel acquisition and cold-junction reporting.
3. Monotonic clock, sequence numbers, structured profile records and persistent logging.
4. Wi-Fi provisioning and live WebSocket or MQTT uplink.
5. Missing-record sync, reboot recovery and profile export.
6. Battery telemetry, internal temperature alarms, watchdog and safe shutdown.

Do not assume live wireless connection exists while the unit is inside the oven. Thermal barrier qualification is a prerequisite to in-oven operation.
