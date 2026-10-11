# Firmware binaries

Version follows Node32-HUB.

## Current release

- **v1.114**: `esp32s3_v1.114_WAVESHARE_<YYYYMMDD_HHMM>.zip` (also on GitHub Releases)

## Build

Compile inside [Node32-HUB](https://github.com/nasp2000/Node32-HUB) with the `Node32-OEE` pack:

```bash
cd chatgpt
pio run -e waveshare_8di8do
```

Post-build output (created by `rename_firmware.py`):

```
build/esp32s3/WAVESHARE/v1.114/<YYYYMMDD_HHMM>/
  esp32s3_v1.114_WAVESHARE_<YYYYMMDD_HHMM>.bin   # + bootloader.bin, partitions.bin, flash_command.txt
  LICENSE, SBOM.md, THIRD_PARTY_NOTICES, README_DISTRIBUTION.txt, third-party.zip
```

## Release

1. Zip `bootloader.bin`, `partitions.bin`, `.bin` and `flash_command.txt` (from the build folder above) → `esp32s3_v1.<ver>_WAVESHARE_<YYYYMMDD_HHMM>.zip`
2. Include the compliance set: `LICENSE`, `SBOM.md`, `THIRD_PARTY_NOTICES`, `README_DISTRIBUTION.txt`, `third-party.zip`
3. Publish the `.zip` as a GitHub Release (the zip itself is not kept on the remote `firmware/` folder)

## Flash

- **First-time**: use [webflasher_Node32-HUB](https://github.com/nasp2000/webflasher_Node32-HUB) (select `esp32s3_v1.114_WAVESHARE_<YYYYMMDD_HHMM>.zip`)
- **Updates**: OTA at `http://<esp32-ip>/ota` (upload only the `.bin` file)
