# Changelog

## v1.0.1

- Fix: crash (assert `getService() != nullptr` / LoadProhibited) when sending reports on ESP32 Arduino core 3.x (NimBLE)
- Root cause: the core's NimBLE-backed BLE wrapper deduplicates characteristics by UUID in `BLEService::addCharacteristic`. HID report characteristics share UUID `0x2a4d`, so the 2nd/3rd ones (keyboard output report, media keys input report) are never registered in the GATT table and their `m_pService` stays uninitialized
- `sendReport(MediaKeyReport*)` now skips the report while the characteristic is unregistered (`getHandle() == 0xFFFF`); a future core fix that registers same-UUID characteristics will re-enable media keys automatically

## v1.0.0

- Initial public release
- BLE HID Keyboard
- Text support
- Key press support
- Multimedia keys