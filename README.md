
# KNOMI-Boykisser
A fork of the BigTreeTech Knomi V2 firmware to replace the dynamic gifs with the Boykisser / Silly Cat meme.

## Important Files
* Gifs can be found in [KNOMI_BOYKISSER_GIFS](./KNOMI_BOYKISSER_GIFS)
* Precompiled boykisser firmware can be found in [KNOMI_BOYKISSER_FIRMWARE_BIN](./KNOMI_BOYKISSER_FIRMWARE_BIN)
* For building, raw firmware source can be found in [KNOMI_BOYKISSER_FIRMWARE](./KNOMI_BOYKISSER_FIRMWARE)

## Building your own
Here's the rundown, Vivi! OwO

## Building KNOMI V2 Firmware

### Prerequisites

- **VSCode** with the **PlatformIO extension**
- **Firmware folder** — To build, open the [KNOMI_BOYKISSER_FIRMWARE_BIN](./KNOMI_BOYKISSER_FIRMWARE_BIN) folder.
- **Espressif Flash Download Tool** (Windows only) — grab it from [espressif.com](https://www.espressif.com.cn/en/support/download/other-tools)
- KNOMI connected via USB directly (no hubs — the ESP32-S3 is picky)

---

### Build Steps

**1. Open the project in VSCode**
Let PlatformIO finish installing dependencies before touching anything.

**2. Fix `platformio.ini`** — this is required or it won't build:

In the `[env:knomiv2]` section:
- Append `@6.4.0` to the `espressif32` platform line
- Add to the end of `lib_deps`:
```
AsyncTCP=esphome/AsyncTCP-esphome@^2.1.1
```

**3. Switch environment** to `knomiv2` in the PlatformIO toolbar (bottom left).

**4. Run Build** (not Upload!) — you should see `SUCCESS`. If not, recheck step 2.

**5. Find your output binaries** at:
```
.pio/build/knomiv2/
  ├── bootloader.bin
  ├── partitions.bin
  └── firmware.bin
```

---

### Flashing

Use the Espressif Flash Download Tool, **not** OTA or PlatformIO Upload:

| File | Offset |
|---|---|
| `bootloader.bin` | `0x0000` |
| `partitions.bin` | `0x8000` |
| `firmware.bin` | `0x10000` |

Settings: **ChipType: ESP32-S3 / WorkMode: Develop / LoadMode: UART**

Hit Start, wait for completion, wait for black screen, then replug. UwU done!

---

### Custom GIFs (optional)

- GIFs must be **240×240px**
- Convert using [lvgl.io/tools/imageconverter](https://lvgl.io/tools/imageconverter) — LVGL8, `CF_RAW_CHROMA`, C array output
- Overwrite the corresponding `.c` file in `/src/gif/`
- Rebuild after swapping





# Original Readme


# KNOMI1

Online manual & customize UI tutorials：[here](https://bigtreetech.github.io/docs/KNOMI.html#)

# KNOMI2

Online manual ：[here](https://bigtreetech.github.io/docs/KNOMI2.html#)

# Klipper config

[KNOMI.cfg](./KNOMI.cfg) is the klipper config of the [latest version firmware](https://github.com/bigtreetech/KNOMI/tree/firmware)

# Firmware source code

[Here](https://github.com/bigtreetech/KNOMI/tree/firmware) is the firmware source code for both KNOMI1 and KNOMI2.

# Firmware update

### OTA

* Download the pre compiled firmware from GitHub([KNOMI1](./KNOMI1/Firmware/knomi1_firmware.bin) and [KNOMI2](./KNOMI2/Firmware/knomi2_firmware.bin)) or build your own firmware
* Enter KNOMI's IP or hostname (default is `knomi.local`) in the browser of a device with the same LAN as knomi, and then click `Update FW`<br/>
  <img src=Images/ota_1.png width="400" /><br/>
* Select the firmware file just downloaded to start updating. After the update is complete, KNOMI will automatically restart and run the new firmware.<br/>
  <img src=Images/ota_2.png width="400" /><br/>

### Using `Flash Download Tools` from Espressif

This step is used when KNOMI1 does not have OTA feature, or KNOMI cannot start and run OTA feature normally

* Refer to the steps [here](https://bigtreetech.github.io/docs/KNOMI.html#update-firmware), but use firmware files from this repository.([KNOMI1](./KNOMI1/Firmware/) and [KNOMI2](./KNOMI2/Firmware/))
