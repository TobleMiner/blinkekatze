Blinkekatze 😺
=============

This is a replacement PCB for one version of cat themed night lights available via various online retailers.

It adds a number of RGB LEDs, sensors and wireless connectivity, enabling an interactive light display synchronized over a large number of Blinkekatzen.

Inspired by the wonderful [derf](https://github.com/derf)

# Architecture

The Blinkekatze is comprised of three PCBs:
 - The mainboard (this directory)
 - The USB board (located in [/usb-board](/usb-board))
 - The original power- and mdoe-switch board from the nightlight

## Mainboard

The mainboard contains most elements critical to device operation. At its heart is an ESP32-C3 for control.

The ESP32-C3 is accompanied by the following peripherals:
 - 16 super bright, individually controllable RGB LEDs (effectively ~12bit RGB color control)
 - High precision battery gauge for accurate capacity tracking and runtime estimation
 - Accelerometer and barometer to detect user interaction
 - Ambient light sensor enabling automatic brightness control
 - Efficient buck-mode battery charger

The mainboard also includes a MEMS PDM microphone that could be used for audio synchronization of lighting effects.
However note the ESP32-C3 is missing hardware PDM to PCM conversion capability.

## USB board

The USB board replaces the original board used for charging in the nightlight. It offers USB connectivity to the
ESP32-C3 and contains two indicator LEDs visible through the bottom of the Blinkekatze.

To facilitate easy, solderless assembly mainboard and USB board are connected by a 5cm long 16 pin flatflex cable wth opposite side contacts.
