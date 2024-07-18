# Sensor Unit

Sensor unit for measuring rain intensity and wind speed.

## Guidline

1. Order PCB by uploading the [Gerber File](pcb/cam/esp-module-su.zip) to [JLCPCB](https://jlcpcb.com/).
2. Order Parts by uploading the [BOM File](pcb/bom/esp-module-su.csv) to [LCSC](https://www.lcsc.com/bom).
3. Build PCB by placing components as visualized in the [BOM Viewer](https://htmlpreview.github.io/?https://github.com/LaCocoRoco/esp-module-su/blob/main/pcb/bom/esp-module-su.html).
4. Download & Install [Git](https://git-scm.com/), [CP210x Driver](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads) and [VSCode](https://code.visualstudio.com/) with [PlatformIO](https://platformio.org/) Extension.
5. Clone the Repository `git clone --recursive https://github.com/LaCocoRoco/esp-module-su.git`.
6. With PlatformIO `Upload Filsystem Image` & `Upload & Monitor ` to your board.

## Module Modes

Modes can be changed by pressing the mode button.  
An audio signal will provide feedback for the active mode.  
Holding the mode button for more than two seconds will clear the module.

### Low Power Mode

- Feedback with one audio signal
- All web functionality is disabled
- Device will enter deep sleep when inactive
- Battery lifetime of several months

### Hybrid Mode

- Feedback with two audio signals
- All web functionality is disabled
- Device will enter deep sleep when battery voltage is below 3.8V
- Battery lifetime of several days

### Web Mode

- Feedback with three audio signals
- All web functionality is enabled
- Battery lifetime of several hours

## Importend

All modules have three different modes: Web Mode, Hybrid Mode, and Low Power Mode.  
The Wi-Fi can be configured as either Access Point or Station Mode.  
However, due to the use of the EspNow protocol for communication, there are some restrictions.

### Modules Set Up as Access Points (Default):

- All modes work without any restrictions.

### Modules Set Up in Station Mode:

- Web Mode works without any restrictions.
- Low Power Mode and Hybrid Mode only work if the Wi-Fi network is set to a **fixed channel**.

### Modules Set Up in Access Point or Station Mode:

- All modes only work if the Wi-Fi network is set to **channel 1**.

## Explanation

The main goal of this project was to avoid reliance on any infrastructure. For configuration, neither an application nor an existing Wi-Fi network is necessary. All modules can be accessed via the corresponding SSID in Access Point Mode or via hostname in Station Mode. However, there are some trade-offs:

To reduce power consumption in Low Power Mode, the module does not establish a direct network connection. It only broadcasts data to the specified receiver. In Station Mode, the network may change the Wi-Fi channel occasionally. Connecting to the network to receive this information would significantly increase uptime.

An alternative approach to this problem would be to scan for the receiver and request the channel. However, this has additional drawbacks:

- Scanning for this information takes some time (though less compared to connecting to a Wi-Fi network).
- It is difficult to distinguish whether a transmission failure is due to the wrong channel or a general network issue.
- Continuously requesting this information until a response is received would quickly add to the uptime and increase power consumption.

This is the reason why the relevant points must be considered mentioned in the [Importand](#importend) section.

## Reference

- [VSCode](https://code.visualstudio.com/) - Lightweight code editor.
- [PlatformIO](https://platformio.org/) - Embedded software development gateway.
- [Autodesk Fusion 360](https://www.autodesk.com/products/fusion-360) - Design and manufacturing software for CAD, CAM, CAE, and PCB.
- [Autodesk Eagle](https://www.autodesk.com/products/eagle) - Electronic design automation software for printed circuit boards.
- [JLCPCB](https://jlcpcb.com/) - Reasonably priced PCB manufacturer.
- [LCSC](https://www.lcsc.com/) - Supplier for a wide selection of electronic components.
- [CP210x Driver](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads) - USB to UART Driver for uploading codebase.
- [InteractiveHtmlBom](https://github.com/openscopeproject/InteractiveHtmlBom) - Bill of materials listing to visually search for components and their placements.

## Preview

![function_graphic](images/esp-module-su-pcb.png)

![function_graphic](images/esp-module-su.png)
