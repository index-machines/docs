<!-- markdownlint-disable-file MD046 -->
# Update the Firmware

All motherboards come pre-flashed with firmware from Opulo and should work out of the box without these steps. If you're setting up a LumenPnP with feeders for the first time, you may need to update your LumenPnP's firmware.

!!! danger "Important"
    It is important that you pick the correct firmware file for your machine.

        - If you have a v2, choose `v2-lumenpnp-firmware-feeder-support.bin`.
        - If you have a v3, choose `v3-lumenpnp-firmware-feeder-support.bin`.

## Option 1: Prebuilt Firmware and STMProgrammer (RECOMMENDED)

The easiest way to update your LumenPnP's motherboard is to use a precompiled binary of the firmware, and the [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html) software by ST.

1. Download the latest [precompiled firmware](https://github.com/opulo-inc/lumenpnp/releases) `.bin` file for your motherboard version.
2. Download and install [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html).
3. Open STM32CubeProgrammer.
4. Select `USB` from the connection type dropdown on the right.
    ![USB Connection drop down](images/usb-connection.png){ loading=lazy }
5. Switch to the "download" tab on the left.
    ![Switch to the download tab](images/download-tab.png){ loading=lazy }

6. Attach the LumenPnP Motherboard to your computer with the included USB cable (USB C to A for Motherboard 3.0, or USB B to A for Motherboard 4.0).

7. Boot your motherboard into DFU Mode
    1. Press and hold the `BOOT` button
    2. Press the `Reset` button and hold for 10 seconds
    3. Release the `Reset` button and wait for 10 seconds
    4. Release the `BOOT` button
  ![Boot and Reset buttons on the motherboard](images/IMG_0749.JPG){ loading=lazy }

    !!! info "NOTE"
        If you have a hard time getting your board to enter DFU mode, instead try powering off the machine entirely, holding the 'BOOT' button, plugging in power, waiting 10 seconds, then release the `BOOT` button.
8. Click the refresh button in the `Port` line to detect the motherboard's port.
    ![Refresh button](images/refresh-button.png){ loading=lazy }

9. Select the newly discovered USB port from the `Port` dropdown menu.
    ![Select USB Port](images/select-port.png){ loading=lazy }

10. Double-check the other fields on the right match the image above:
    1. `PID: 0xdf11`
    2. `VID: 0x0483`
    3. `Read Unprotect (MCU): Unchecked`
    4. `TZEN Regression (MCU): Unchecked`

11. Click the green `Connect` button to connect to the motherboard.
    ![Connect to Motherboard button](images/connect-to-motherboard.png){ loading=lazy }

12. Click the `Browse` button to browse for the binary you downloaded earlier.
    ![Click the browse button](images/browse-for-binary.png){ loading=lazy }

13. Click the `Start Programming` button to upload the firmware to the motherboard.
    ![Start Programming the motherboard](images/start-programming.png){ loading=lazy }

14. Let the upload finish.
    ![Upload finished](images/upload-done.png){ loading=lazy }

15. Press the `reset` button on the motherboard to reboot it.

16. The machine should show up as a COM/Serial Port on your PC now, and you should be able to access it via OpenPNP. If it doesn't, press the Reset button on the board again, or power-cycle the machine *after the flashing is completed*.

This is how you can check whether your machine is connected properly:

* Windows: ![Device manager](images/STM32_COM_port_connected.png){ loading=lazy }
* Mac/Linux: ![Terminal lsusb](images/linux_lsusb.png){ loading=lazy }

## Option 2: Auto Build Marlin and `dfu-util`

!!! info "Marlin"
    Building an older version of Marlin with the recommended config files won't work. If you are unsure whether a previously-downloaded local version of Marlin is the newest one, re-downloading it is the safest choice.

1. Download the [latest Marlin firmware][marlin] and unzip it.
2. Install [VSCode][vscode] and its [PlatformIO extension][pIO].
3. Open Marlin firmware's folder in VSCode.
4. Download the Marlin configuration files [here][marlin-config] and
5. Replace the files in the `Marlin/Marlin` folder from step #1 with the new configuration files from step #4.
6. Install the Auto Build Marlin plugin using this [Marlin Documentation page][marlin-docs], or download it directly from the [Visual Studio Marketplace][abmvs].
7. Install `dfu-util`
8. Try to build Marlin using the build button with the hammer icon as shown below. See [Troubleshooting](#troubleshooting-building-with-auto-build-marlin) for more help
    ![Marlin Auto Build screenshot](images/marlin-auto-build-ui.png){ loading=lazy }

9. Attach the LumenPnP Motherboard to your computer with the included USB cable (USB C to A for Motherboard 3.0, or USB B to A for Motherboard 4.0).

10. Boot your motherboard into DFU Mode
    1. Press and hold the `BOOT` button
    2. Press the `Reset` button and hold for 10 seconds
    3. Release the `Reset` button and wait for 10 seconds
    4. Release the `BOOT` button
  ![Boot and Reset buttons on the motherboard](images/IMG_0749.JPG){ loading=lazy }

    !!! info "NOTE"
        If you have a hard time getting your board to enter DFU mode, instead try powering off the machine entirely, holding the 'BOOT' button, plugging in power, waiting 10 seconds, then release the `BOOT` button.

11. In the integrated terminal in the root of the repository, flash the Motherboard using `dfu-util` by running the command:

    ```shell
    dfu-util -d 0x0483:0xdf11 -s 0x08000000:leave -a 0 -D ./.pio/build/Opulo_Lumen_REV3/firmware.bin
    ```

    ![command prompt in vs code](images/vscode-dfu-util-integrated-terminal.png){ loading=lazy }
    !!! info "COMMAND EXPLANATION"
        `dfu-util` is a flash tool available on all platforms.

        * `-d 0x0483:0x0df11` tells the tool to flash the STM32 chip on the motherboard. This is optional if you only have one dfu device connected.
        * `-s 0x8000000:leave` is the target memory address that the firmware is flashed to. The `:leave` part will cause the chip to reset on its own, making the machine accessible in OpenPNP without rebooting it.
        * `-a 0` makes the tool use the alt setting required for flashing the ESP32.
        * `-D ./.pio/build/Opulo_Lumen_REV3/firmware.bin` is the path to the to-be-flashed firmware. If you want to flash another file, change this.

12. Wait for the process to finish.

13. The machine should show up as a COM/Serial Port on your PC now, and you should be able to access it via OpenPNP. If it doesn't, press the Reset button on the board, or power-cycle the machine *after the flashing is completed*.

 This is how you can check whether your machine is connected properly:

* Windows: ![Device manager](images/STM32_COM_port_connected.png){ loading=lazy }
* Mac/Linux: ![Terminal lsusb](images/linux_lsusb.png){ loading=lazy }

## Option 3: Auto Build Marlin Only

Note that flashing the firmware using the Auto Build Marlin Plugin might work, but seems error-prone for most people. We recommend using `dfu-util` as described above. Here are the steps to use Auto Build Marlin if you'd like to try it.

1. Download the [latest Marlin firmware][marlin] and unzip it.
2. Install [VSCode][vscode] and its [PlatformIO extension][pIO].
3. Open Marlin firmware's folder in VSCode.
4. Download the Marlin configuration files [here][marlin-config].
5. Replace the files in the `Marlin/Marlin` folder from step #1 with the new configuration files from step #4.
6. Install the Auto Build Marlin plugin using this [Marlin Documentation page][marlin-docs], or download it directly from the [Visual Studio Marketplace][abmvs].
7. Try to build Marlin using the build button with the hammer icon as shown below. See [Troubleshooting](#troubleshooting-building-with-auto-build-marlin) for more help.
    ![Marlin Auto Build screenshot](images/marlin-auto-build-ui.png){ loading=lazy }

8. Attach the LumenPnP Motherboard to your computer with the included USB cable (USB C to A for Motherboard 3.0, or USB B to A for Motherboard 4.0).
9. Boot your motherboard into DFU Mode
    1. Press and hold the `BOOT` button
    2. Press the `Reset` button and hold for 10 seconds
    3. Release the `Reset` button and wait for 10 seconds
    4. Release the `BOOT` button
    ![Boot and Reset buttons on the motherboard](images/IMG_0749.JPG){ loading=lazy }

10. Now, press the upload button in ABM as shown below:
    ![Auto Marlin Build screenshot](images/marlin-auto-build-ui.png){ loading=lazy }

11. Wait for the process to finish
12. The machine should show up as a COM/Serial Port on your PC now, and you should be able to access it via OpenPNP. If it doesn't, press the Reset button on the board, or power-cycle the machine *after the flashing is completed*.

This is how you can check whether your machine is connected properly:

* Windows: ![Device manager](images/STM32_COM_port_connected.png){ loading=lazy }
* Mac/Linux: ![Terminal lsusb](images/linux_lsusb.png){ loading=lazy }

## Option 4: PlatformIO

1. Download the [latest Marlin firmware][marlin] and unzip it.
2. Install [VSCode][vscode] and its [PlatformIO extension][pIO].
3. Open Marlin firmware's folder in VSCode.
4. Download the Marlin configuration files [here][marlin-config].
5. Replace the files in the `Marlin/Marlin` folder from step #1 with the new configuration files from step #4.
6. Edit the `platformio.ini` file to indicate which board you're uploading to. Update `default_envs` to read `Opulo_Lumen_REV3` or `Opulo_Lumen_REV4` depending on your motherboard.
  ![editing platformio.ini](images/Screen Shot 2022-02-04 at 7.27.25 PM.png){ loading=lazy }
7. Attach the LumenPnP Motherboard to your computer with the included USB cable (USB C to A for Motherboard 3.0, or USB B to A for Motherboard 4.0).
8. Boot your motherboard into DFU Mode
    1. Press and hold the `BOOT` button
    2. Press the `Reset` button and hold for 10 seconds
    3. Release the `Reset` button and wait for 10 seconds
    4. Release the `BOOT` button
    ![Boot and Reset buttons on the motherboard](images/IMG_0749.JPG){ loading=lazy }

    !!! info "NOTE"
        If you have a hard time getting your board to enter DFU mode, instead try powering off the machine entirely, holding the 'BOOT' button, plugging in power, waiting 10 seconds, then release the `BOOT` button.

9. Upload firmware to the board via PlatformIO:
    ![Upload button in PlatformIO](images/vscode_marlin_env.png){ loading=lazy }

10. Wait for the process to finish:
    ![Terminal Output for uploading](images/PIO_upload_done.png){ loading=lazy }

11. The machine should show up as a COM/Serial Port on your PC now, and you should be able to access it via OpenPNP. If it doesn't, press the Reset button on the board, or power-cycle the machine *after the flashing is completed*.

This is how you can check whether your machine is connected properly:

* Windows: ![Device manager](images/STM32_COM_port_connected.png){ loading=lazy }
* Mac/Linux: ![Terminal lsusb](images/linux_lsusb.png){ loading=lazy }

## Flashing Factory Firmware

If you've put new firmware on your motherboard, but just want to get back to the firmware that your machine was flashed with, check the release for your build number and download the .bin firmware file attached to it. Put your board into DFU mode as described above, connect to your computer, and flash the binary to the board using the following command:

```shell
`dfu-util -d 0x0483:0xdf11 -s 0x08000000:leave -a 0 -D ~/path/to/firmware.bin`
```

Once flashing is completed, the machine should automatically exit DFU mode, and be accessible to OpenPNP again.

## Troubleshooting

### Troubleshooting Building with Auto Build Marlin

If you can't build with the Auto Build Marlin tool:

1. Check the error messages for configuration errors and fix them, or replace it with the default config
2. If this fails, check that your config file version is the same as your Marlin version (e.g. a bugfix-2.0.x config file won't work in a bugfix-2.1.x)
3. When in doubt, re-download Marlin and the configuration files from the links above

### Other Troubleshooting

If you aren't able to upload, you can check to see if your motherboard is booting into DFU mode correctly:

* Windows: ![Device Manager](images/dfu_mode_device_manager.png){ loading=lazy }
* Mac/Linux: ![lsusb output](images/linux_lsusb_bootloader.png){ loading=lazy }

Also, reference [the Marlin instructions for uploading](https://marlinfw.org/docs/basics/install_platformio.html).

## Next steps

Continue to [wiring and pneumatics](../../wiring-and-pneumatics/wiring-y-motors/index.md).

[abmvs]: https://marketplace.visualstudio.com/items?itemName=MarlinFirmware.auto-build
[marlin-docs]: https://marlinfw.org/docs/basics/auto_build_marlin.html
[marlin-config]: https://github.com/MarlinFirmware/Configurations/tree/import-2.1.x/config/examples/Opulo/Lumen_REV4
[marlin]: https://github.com/MarlinFirmware/Marlin/
[vscode]: https://code.visualstudio.com/
[pIO]: https://marketplace.visualstudio.com/items?itemName=platformio.platformio-ide
