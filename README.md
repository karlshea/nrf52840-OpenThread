# OpenThread [nRF52840](https://mou.sr/3AkvVTz) Firmware Builder

This repository automatically builds the latest version of the OpenThread firmware for the nRF52840 platform. The firmware includes both UART and USB versions, which can be downloaded directly from the **Actions** tab in this GitHub repository.

## Overview

The build process ensures the most up-to-date OpenThread firmware for nRF52840 by leveraging GitHub Actions. Both versions of the firmware (UART and USB) are built and tagged accordingly:

- **UART Version**: `ot-cli-ftd-UART.hex`
- **USB Version**: `ot-cli-ftd-USB.hex`

The firmware is uploaded as artifacts that you can download directly from the **Actions** tab.

## How to Download the Firmware

1. Go to the [**Actions tab**](../../actions) of this repository.
2. Select the latest workflow run for the `Build OpenThread nRF52840 Examples` workflow.
3. Scroll down to the **Artifacts** section at the bottom of the workflow page.
4. Click on the `ot-nrf528xx-binaries` artifact to download a ZIP file containing:
   - `ot-cli-ftd-UART.hex`
   - `ot-cli-ftd-USB.hex`
   - Corresponding ELF files.

## How to Flash the Firmware

### USB Version

To flash the USB version (`ot-cli-ftd-USB.hex`), you can use either the **nRF Connect for Desktop** application or the **nrfjprog** command-line tool. Follow the steps below based on your preferred method:

#### Using nRF Connect for Desktop

1. Download and install [nRF Connect for Desktop](https://www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-desktop) if not already installed.
2. Launch **nRF Connect for Desktop** and open the **Programmer Tool**.
3. Put the nRF52840 dongle into **program mode**:
   - Insert the dongle into a USB port on your computer.
   - Hold down the reset button while inserting the dongle until the LED blinks rapidly. This indicates the device is in program mode.
4. In the Programmer Tool, select the detected nRF52840 dongle from the device list.
5. Click **Add file** and choose the `ot-cli-ftd-USB.hex` file.
6. Ensure the **Erase & Write** option is selected.
7. Click **Write** to flash the firmware onto the dongle.

#### Using nrfjprog

If you prefer using the command-line tool, **nrfjprog** (part of the [nRF Command Line Tools](https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF-Command-Line-Tools)) can also flash the USB firmware.

1. Put the nRF52840 dongle into **program mode**:
   - Insert the dongle into a USB port.
   - Hold down the reset button while inserting it, until the LED starts blinking rapidly.

2. Flash the USB firmware:
   - Use the following command:
     ```bash
     nrfjprog --program ot-cli-ftd-USB.hex --sectorerase --reset
     ```

3. Verify the flashing process:
   - After flashing, the device should start running the new firmware.

**Note**: The `--sectorerase` flag ensures only the necessary sectors are erased, preserving the bootloader on the USB dongle.

### UART Version

Once you have downloaded the firmware, you can flash it onto your nRF52840 device using `nrfjprog` (part of the [nRF Command Line Tools](https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF-Command-Line-Tools)):

```bash
nrfjprog -f nrf52 --chiperase --program ot-cli-ftd-UART.hex --reset
```

## License

This repository and the OpenThread firmware are licensed under the [BSD 3-Clause License](LICENSE).

## Links

- [OpenThread Documentation](https://openthread.io/)
- [nRF52840 Product Page](https://www.nordicsemi.com/Products/nRF52840)
- [nRF Command Line Tools](https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF-Command-Line-Tools)
- [nRF Connect for Desktop](https://www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-desktop)
