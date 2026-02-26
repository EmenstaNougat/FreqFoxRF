<h1 align="center">FreqFoxRF - by @emensta</h1>
<div align="center">
  <img width="1198" height="689" alt="image" src="https://github.com/user-attachments/assets/e256659e-9615-4333-8ece-9c7cbe481b3d" />
  <h3 align="center">Intended for authorized testing, research, and educational use only!</h3>
</div>

---
A portable sub-GHz RF signal Multi-Tool built on the ESP32-C3 SuperMini with a CC1101 radio module, created to push the boundaries. FreqFoxRF scans, detects, logs, and replays wireless signals across common ISM bands - all from a compact handheld device with a 128×64 OLED display and 5-button navigation.

#### STILL IN DEVELOPMENT!

## Features

- **Frequency Analyzer** - scans 10 bands across 300–915 MHz, auto-detects active frequencies with hot-dwell burst locking and a 2-second confirmation window before logging
- **Live Spectrum Monitor** - real-time RSSI energy display with scrolling history, peak hold, and per-band sensitivity tuning (315 / 433 / 868 / 915 MHz)
- **Signal Capture** - captures and stores OOK/ASK signals with protocol detection
- **Raw Capture** - records raw pulse timings for signals that don't match known protocols
- **Signal Replay** - retransmit any captured or saved signal
- **Brute Force** - sequential code transmission for compatible receivers (not added yet)
- **Saved Signals** - persistent signal storage in EEPROM, survives power cycles
- **Jammer Detector** - detects abnormal RF noise levels on monitored frequencies (not added yet)
- **Adjustable Sensitivity** - UP/DOWN buttons tune the RSSI threshold live on both the analyzer and capture screens

---

## Hardware

| Component | Details |
|---|---|
| MCU | ESP32-C3 SuperMini |
| Radio | CC1101 sub-GHz transceiver module |
| Display | 128×64 OLED (I2C, SSD1306) |
| Navigation | 5 push buttons |
| Power | USB-C or LiPo via ESP32-C3 onboard regulator |

### Pin Wiring (NOT FINAL! Hardware will be added, therefore pins may be changed in the future!)

| Signal | ESP32-C3 Pin |
|---|---|
| CC1101 SCK | GPIO 4 |
| CC1101 MISO | GPIO 5 |
| CC1101 MOSI | GPIO 6 |
| CC1101 CSN | GPIO 7 |
| CC1101 GDO0 | GPIO 2 |
| OLED SDA | GPIO 8 |
| OLED SCL | GPIO 9 |
| Button UP | GPIO 1 |
| Button DOWN | GPIO 3 |
| Button LEFT | GPIO 10 |
| Button RIGHT | GPIO 20 |
| Button SELECT | GPIO 21 |

---

## Supported Frequency Bands

| Band | Typical Devices |
|---|---|
| 300 MHz | Generic ISM remotes |
| 303 / 308 MHz | Genie Intellicode, US alarm fobs |
| 310 / 315 / 318 MHz | Toyota, Honda, GM fobs, Chamberlain, LiftMaster |
| 330 / 345 MHz | Honeywell, 2GIG alarm sensors |
| 390 MHz | Older OOK remotes |
| 418 MHz | UK/EU ISM : alarm PIRs, door sensors |
| 430 MHz | EU/JP garage remotes |
| 433 MHz | EU standard : remotes, sensors, LoRa |
| 868 MHz | Z-Wave EU, LoRaWAN, wireless M-Bus, Sigfox |
| 915 MHz | Z-Wave US, LoRaWAN US915, smart meters |

---

## Installation

The source code is not made publicly available due to ungrateful individuals that previously stole my projects to profit from the sale of my devices without any attribution, ignoring the included project license. Install FreqFoxRF by flashing the pre-compiled binary. Hopefully we will warp into a future where such consequences are not required...

### Option 1 - esptool (Command Line)

Make sure Python and esptool are installed:

```bash
pip install esptool
```

Then flash with:

```bash
esptool.py --chip esp32c3 --port /dev/ttyUSB0 --baud 460800 \
  write_flash -z 0x0 FreqFoxRF.bin
```

> Replace `/dev/ttyUSB0` with your actual serial port (`COM3`, `/dev/tty.usbserial-*`, etc.)

To erase the chip before flashing (recommended for first install):

```bash
esptool.py --chip esp32c3 --port /dev/ttyUSB0 erase_flash
```

### Option 2 - ESP Flash Download Tool (Windows GUI)

1. Download the [ESP Flash Download Tool](https://www.espressif.com/en/support/download/other-tools) from Espressif
2. Select chip: **ESP32-C3**
3. Add `freqfoxrf.bin` at offset `0x0`
4. Select your COM port, set baud to `460800`
5. Click **START**

### Option 3 - Web Flasher

A browser-based flasher (no drivers required) may be available via [ESP Web Tools](https://esphome.github.io/esp-web-tools/) - check the releases page for a hosted installer link.

---

## Notes

- The CC1101 uses OOK energy detection for RSSI-based scanning across all bands, this allows reliable detection of both OOK and FSK devices without needing to match modulation
- 868 MHz detection requires the device to be reasonably close to the signal source due to the CC1101's reduced sensitivity above 700 MHz
- Saved signals persist across reboots via EEPROM (up to 20 signals, 2048 bytes total)
- Raw capture stores pulse timings for signals that fall outside known protocol formats
- in active development, features will be added!

---

## UI & Display

The FreqFoxRF display graphics were designed using **[Lopaka](https://lopaka.app)** - a free, browser-based UI editor for embedded displays. If you're building anything that makes pixels go "Beep, Boop! 0 1", Lopaka lets you visually design your layouts and exports ready-to-use code directly. No more guessing pixel coordinates by hand.

Seriously worth bookmarking if you do any embedded UI work: **https://lopaka.app**
Special thanks to Lopaka.app for sponsoring and supporting by this!

---

## Disclaimer

FreqFoxRF is intended for authorized testing, research, and educational use only. Transmitting on licensed frequencies without authorization may be illegal in your jurisdiction. I, The author (@emensta) DO NOT take responsibility for misuse.

---

## License

Hardware design and firmware are proprietary. Binary releases are provided for personal, non-commercial use only. Redistribution of the binary without permission is not permitted.
