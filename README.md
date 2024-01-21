Blinkekatze 😺
=============

This is a replacement PCB for one version of cat themed night lights available via various online retailers.

It adds a number of RGB LEDs, sensors and wireless connectivity, enabling an interactive light display synchronized over a large number of Blinkekatzen.

Inspired by the wonderful [derf](https://github.com/derf)

# Architecture

The Blinkekatze is comprised of three PCBs:
 - The main board (this directory)
 - The USB board (located in [/usb-board](/usb-board))
 - The original power- and mode-switch board from the nightlight

## Mainboard

The main board contains most elements critical to device operation. At its heart is an ESP32-C3 for control.

The ESP32-C3 is accompanied by the following peripherals:
 - 16 super bright, individually controllable RGB LEDs (effectively ~12bit RGB color control)
 - High precision battery gauge for accurate capacity tracking and runtime estimation
 - Accelerometer and barometer to detect user interaction
 - Ambient light sensor enabling automatic brightness control
 - Efficient buck-mode battery charger

The main board also includes a MEMS PDM microphone that could be used for audio synchronization of lighting effects.
However note the ESP32-C3 is missing hardware PDM to PCM conversion capability.

## USB board

The USB board replaces the original board used for charging in the nightlight. It offers USB connectivity to the
ESP32-C3 and contains two indicator LEDs visible through the bottom of the Blinkekatze.

To facilitate easy, solderless assembly mainboard and USB board are connected by a 5cm long 16 pin flat flex cable with opposite side contacts.

# Ordering PCBs

All PCBs required to build Blinkekatzen can be ordered fully assembled from JLCPCB. The necessary fabrication files are located in [/fab](/fab) for
the main board and [/usb-board/fab](/usb-board/fab). It is recommended to always use the latest revision available in those folders.  
When ordering the PCBs they should be ordered as 1.6mm 4 layers for the mainboard and 1.6mm 2 layers for the USB board.

## PCB assembly

In addition to the bare PCBs JLCPCB also offers an assembly service. The BOM and component centroid files required for assembly are also located in
[/fab](/fab) and [/usb-board/fab](/usb-board/fab) respectively.  
When ordering assembly for the main PCB cost can be reduced significantly by choosing to populate only the top side of the PCB and later assembling
the battery contacts (BTT1 and BTT2) on the bottom side by yourself manually. Those are the only parts on the bottom side of the PCB. Also microphone
U6 is best left unpopulated since a lack of proper PDM to PCM support on the ESP32-C3 makes it mostly unusable.

### Additional required electronic components

Apart from the components assembled by JLCPCB the following parts are required:  
 - 2x MYOUNG MY-18650-01 battery contacts (if not assembled by JLCPCB, see previous section)
 - 1x 5cm 16pin 0.5mm pitch flat flex cable (e.g. C5151983 on LCSC)
 - 1x 18650 battery (Samsung INR18650-35E recommended)

### JLCPCB assembly component availability

Sometimes components required for assembly are out of stock at JLCPCB. In this case the parts have to be ordered fist through
JLCPCB's parts preorder service. Usually all required parts can be preordered in small quantities and will be available within
a couple of days.

# Assembling the Blinkekatzen

## Preparing the PCB

If the battery contacts were not assembled through JLCPCB they need to be soldered. The overall fit of the battery is best with the
contacts installed as far apart as possible within the throughholes. Special care should be taken to ensure the battery contacts are
not soldered at an angle but lie flat on the PCB. Otherwise the battery might not snap into the contacts properly.

## Preparing the housing

In the first step the rubber boot needs to be removed. The puck containing all electronics can either be pulled out to the bottom or
first pushed into the puck and then removed.  
Next the transparent diffuser on top of the puck can be removed by undoing the three screws (relatively long and skinny #0 Phillips
head screwdriver required) and pulling up on the diffuser.  

## Removing the original PCBs

The original PCB is held in place with two screws. After undoing the screws the PCB can be pivoted to the side and the battery unplugged.  
The original USB board also needs to be removed by undoing the two screws holding it in place.  
Finally the PCB can be freed by desoldering the six connections on the original main PCB that go to the switch board in the bottom of the case.
Since the switch board will be reused desoldering rather than cutting the wire can save some time later.  

## Modifying the case

After removal of the original main PCB the case needs to be modified slightly to accommodate the new battery. To make space for the new battery
and battery holder snip out the two thin plastic walls with the half circle shaped cutouts the old battery was resting on using flush cutters.

## Installing the USB board

The first new component to be installed in the housing is the new USB board. Since this board will be installed with the USB connector and flat
flex connector facing down the flat flex cable needs to be connected to this board first. To connect the flat flex cable the latch on the
connector must be flipped up and the cable then inserted with the contacts facing down. The cable is then secured by closing the latch again.  
Now the USB board can be installed in the housing and secured in place with the two screws.

## Installing the new main PCB

As a first step the two outermost contacts of the ribbon cable earlier desoldered from the original main PCB are soldered to the power key header
J1 on the new main PCB (labeled PWR_ON and VBAT, polarity does not matter). Then the battery is installed (here polarity does very much matter). **NEVER**
may batteries without or with a damaged insulating sleeve be used with this device. The battery contacts will short out such batteries!  
After folding back the flat flex cable so it remains free and is not trapped under the battery the new main PCB is fixed in place with two screws.  
As a final step the flat flex cable is now installed into the flat flex connector on the new main PCB in the same manner as on the USB board.

## Firmware flashing

Please see [blinkekatze-firmware](https://github.com/TobleMiner/blinkekatze-firmware) for details on firmware flashing.
