# microbit-corona-scanner
The micro:bit finds BLE Beacons according to the Google/Apple COVID-19 Exposure Notification specification (https://www.blog.google/documents/70/Exposure_Notification_-_Bluetooth_Specification_v1.2.2.pdf)

LEDs indicate received Exposure Notification beacons (or BLE devices - see below).<br/>
There's one LED per Rolling Proximity Identifier (RPI) so up to 25 active RPIs with all 25 LEDs.

## Video
[![usage video](https://img.youtube.com/vi/39K_UgLI7oA/0.jpg)](https://www.youtube.com/watch?v=39K_UgLI7oA)

## Usage
### BBC micro:bit
![microbit](https://raw.githubusercontent.com/znuh/microbit-corona-scanner/master/docs/microbit_en.png)
### BBC micro:bit (german)
![microbit](https://raw.githubusercontent.com/znuh/microbit-corona-scanner/master/docs/microbit.png)
### Calliope Mini (german)
![calliope](https://raw.githubusercontent.com/znuh/microbit-corona-scanner/master/docs/calliope.png)

### Text description
The number of devices is output every ~8 seconds via the USB serial port.

Press **B** to change **visualisation mode**:
 * 0: persistence with fadeout from RSSI				[DEFAULT]
 * 1: blink with RSSI brightness (one blink per RX event)
 * 2: persistence at full brightness (useful in sunlight)
 * 3: blink at full brightness (one blink per RX event - useful in sunlight)

Press **B** for **3 seconds** to see **all BLE devices**, not just COVID-19 Exposure Notifications.<br/>
Press again for 3 seconds to switch back to COVID-19 Exposure Notifications only.<br/>
When visibility of all BLE devices is enabled LEDs blinking at 2Hz are COVID-19 Exposure Notifications, the rest is other devices.

Press **A** to toggle **sound output**.<br/>
Beacons from the device with the strongest signal do not trigger a click.<br/>
**BBC micro:bit**: connect headphones to **PAD 0** and **GND**.<br/>
**Calliope Mini**: connect headphones to **PAD 1** and **GND**.<br/>
You can also use the builtin speaker of the Calliope Mini: Pressing **A** the first time enables headphones output, pressing **A** again switches to speaker output, a third press turns sound output off again.

Press **A** for **3 seconds** to see **received Data via USB** serial port.<br/>
Press again for 3 seconds to disable.

## How to Build
This project uses yotta to build, not pxt.<br/>
This project uses the another SoftDevice(S130). That enables BLE Central feature.

Follow these steps to build the project.<br/>
** Don't forget copying NRF51822_S130.ld to NRF51822.ld ! **

```bash
# set target to use S130 SoftDevice.
yotta target bbc-microbit-classic-gcc-s130

# the linker uses `NRF51822.ld` file, then copy `NRF51822_S130.ld` to `NRF51822.ld`.
cp NRF51822_S130.ld yotta_targets/bbc-microbit-classic-gcc-s130/ld/NRF51822.ld

# build the project
yotta build

# transfer the hex file to micro:bit. (for example, macOS X)
cp build/bbc-microbit-classic-gcc-s130/source/corona-scanner-combined.hex /Volumes/MICROBIT/
```

## Building on Ubuntu Linux
sudo apt install yotta ninja-build srecord

## Building on Windows
get https://launchpad.net/gcc-arm-embedded/+download for arm gcc  
get https://github.com/ninja-build/ninja for building with cmake  
get https://sourceforge.net/projects/srecord/ for linking   

