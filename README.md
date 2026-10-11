# Node32-OEE

**OEE and production-counting firmware for ESP32-S3 Waveshare 8DI8DO (PoE Ethernet)** — part of the [Node32-HUB](https://github.com/nasp2000/Node32-HUB) project.

> ⚠️ Current release targets **ESP32-S3 Waveshare 8DI8DO POE only**.

Industrial production monitor built on the **Waveshare 8DI8DO**. Eight opto-isolated digital inputs read PNP/NPN proximity sensors, encoders and relays and turn them into counters, presence detection and speed, with automatic shift management, CSV reports to SD, and real-time **OEE** (Availability × Performance × Quality) per channel. Runs on **Ethernet (W5500)** with email alerts.

<table>
  <tr>
    <td width="50%"><img src="image/oee.png" width="100%" alt="Node32-OEE production / OEE page"></td>
    <td width="50%"><img src="image/csv.png" width="100%" alt="Node32-OEE shift CSV report"></td>
  </tr>
</table>

📷 [More screenshots](image/)

---

## Features

### Production counting (`/proximity`)
- **8 independent channels** (DI1…DI8), each PNP/NPN
- **COUNTER** mode — pulse counting (Count IN / Count OUT), with optional relay pulse output
- **PRESENCE** mode — live ON/OFF detection only
- **SPEED** mode — pulses-per-minute and cycle time between pulses
- **Shift management** — automatic shift transitions, CSV reports to SD, SHIFTDAY email command
- **OEE** — Availability × Performance × Quality per channel, with per-channel targets

### Live dashboard (`/proximity-dashboard`)
- Read-only, TV-style wallboard: one 24-hour per-hour chart per channel in use, rendered locally on canvas
- Real-time **OEE / A / Q / P** row with the current-shift indicator
- Light theme, designed for a big screen in the factory, auto-refresh every 2 s

### Alerts (`/alerts-config`)
- **Inactivity alerts** — up to 6 slots email when a channel stops receiving data for 5 min → 24 h
- **OEE alerts** — up to 3 slots email when Shift/Day OEE or Availability stays below target (with a per-day cap)

### Network & storage
- **Ethernet (W5500)** + Wi-Fi AP/station with HTTP Basic Authentication
- **SD card storage** — shift CSV reports and logs under `/`
- **File manager** and SD card pages + **FTP client** uploads
- **Monitor page** — live web serial/status monitor
- NTP time sync, OTA updates, scheduled daily reboot

---

## Hardware Recommendation

[**Waveshare ESP32-S3 8DI8DO POE**](https://www.waveshare.com/esp32-s3-8di8do-poe.htm) — 8 opto-isolated digital inputs, 8 relay outputs, W5500 Ethernet and PoE.

The only tested board. The digital inputs map directly to the proximity/encoder channels (DI1…DI8).

---

## Quick start

1. Flash the pre-built binary to your ESP32-S3 8DI8DO (binaries in Releases) using [webflasher_Node32-HUB](https://github.com/nasp2000/webflasher_Node32-HUB). For future updates use **OTA** at `http://<esp32-ip>/ota`
2. Connect the board over **Ethernet (PoE)** and wire your sensors to DI1…DI8
3. Open `http://node32-oee.local/proximity` in a browser (mDNS — follows the System Name) or `http://<esp32-ip>/proximity`, and log in (default `root`/`root`)
4. Configure each active channel (mode, sensor type, shift times) and watch counts / OEE on the dashboard

---

## First Access

1. Flash the pre-built binary
2. Wait for AP **NODE32-HUB**
3. Connect with password **12345678**
4. Browse to `http://192.168.4.1`
5. Login with user **root** / password **root**
6. Go to **Settings → Wi-Fi** and connect to your local network (or use Ethernet)
7. Once connected, the AP turns off automatically and the device is reachable at `http://node32-oee.local` (mDNS — follows the System Name) or the assigned IP

> If the device loses connection to the network, it reactivates AP mode automatically.

---

## License

Released under the MIT License — see [LICENSE](https://github.com/nasp2000/Node32-HUB/blob/main/LICENSE) in the main repository. This firmware links LGPL-2.1/LGPL-3.0 libraries; see [THIRD_PARTY_NOTICES](https://github.com/nasp2000/Node32-HUB/blob/main/THIRD_PARTY_NOTICES).
