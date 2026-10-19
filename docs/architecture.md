# System architecture and data contract — draft

## Device
ESP32-S3 + 8 x MAX31856 + local NOR log storage + independent temperature/power monitoring.
Initial sampling target 2–5 Hz/channel. Thermocouple conversion completion and bus timing must be confirmed.

## Data pipeline
Thermocouple acquisition -> timestamp and sequence -> persist record locally -> queue Wi-Fi packet -> receiver -> live GUI.
Transmission is best effort. Stored records are authoritative. After the run the host requests missing sequence ranges; duplicate records are safely ignored.

## Suggested packet (illustrative JSON)
```json
{
  "version": 1,
  "device_id": "profiler-001",
  "session_id": "run-001",
  "sequence": 42,
  "elapsed_ms": 8400,
  "temperatures_c": [120.1, 119.9, 121.0, 118.7, 120.5, 119.6, 122.2, 120.0],
  "internal_c": 34.2,
  "battery_v": 3.9,
  "fault_bits": 0
}
```
Production serialization may use CBOR/protobuf for lower overhead. Record schema must include channel-level sensor faults, acquisition interval and calibration metadata. Use CRC for persisted frames.

## Host
Windows-first application, optionally Raspberry Pi/web dashboard. Plot actual thermal profile; compute peak, soak, time above liquidus, heating/cooling ramp rates and paste window. Store calibration and oven recipes.

## Prediction
Start with measured profiles; fit and cross-validate thermal response models for actual PCB and Heller 1809 MK7 recipes. Predictions are advisory and require a verification run. Keep nine upper and nine lower heating zone setpoints distinct where controllable. No oven control integration until interfaces and permissions verified.
