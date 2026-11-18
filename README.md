# Bruce Remote

Unofficial Android BLE remote and screen mirror for LilyGO T-Embed CC1101 running Bruce firmware.

Control your Bruce device and view its live display directly from your Android phone over Web Bluetooth — no Wi-Fi, USB, or companion app required.

## Hardware

LilyGO T-Embed CC1101 with Bruce firmware. BLE API must be enabled on the device before pairing:

**Config → Advanced → Toggle BLE API**

## Features

- Real-time screen mirroring at 320×170 — parses Bruce's live TFT draw-call stream onto an HTML5 Canvas
- Full hardwareless control — D-Pad mapped to the rotary encoder (PREV/UP, NEXT/DOWN), SELECT, and BACK/ESC
- Long press with auto-repeat on navigation keys
- Screen repaint — forces the device to redraw the current frame
- Interactive BLE terminal for raw CLI commands (`info`, `free`, `uptime`, etc.)
- Connection, disconnection, reconnection, and connection status indicators
- Battery level readout via BLE Battery Service

## BLE Protocol

| Service / Characteristic | UUID | Role |
| :--- | :--- | :--- |
| NUS Service | `6e400001-b5a3-f393-e0a9-e50e24dcca9e` | Primary BLE service |
| NUS RX (write) | `6e400002-b5a3-f393-e0a9-e50e24dcca9e` | App → Bruce |
| NUS TX (notify) | `6e400003-b5a3-f393-e0a9-e50e24dcca9e` | Bruce → app |
| Battery Service | `0x180F` / `0x2A19` | Battery level |
| Bruce Serial (fallback) | `4371ec0b-...` / `d555ed97-...` | Alternative firmware layout |

Commands end with `\r\n`. Navigation uses `nav <dir> [duration]`, e.g. `nav sel 600` for long press. Screen streaming is enabled with `display start` / `display stop`.

## Installation

Open `index.html` in Google Chrome on Android. Tap **Connect** and select your `Bruce` / `Bruc` device from the scanner dialog.

Web Bluetooth requires:
- Bluetooth enabled
- Location services enabled (Android requirement for BLE scanning)
- Secure context (HTTPS or localhost)


## Protocol reference

Based on [BruceDevices/App-IOS](https://github.com/BruceDevices/App-IOS) and the Bruce firmware `tftLogger` binary draw packet format (`0xAA`-prefixed packets, big-endian arguments).

## License

AGPL-3.0
