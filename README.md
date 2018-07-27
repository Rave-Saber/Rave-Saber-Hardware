# RaveSaber - AVR Hardware

This repository contains the hardware schematics, parts list, & eventual PCB
files for the RaveSaber electronics.

Currently we only have a simple breadboard setup for testing the firmware code.

![A Schematic Drawing of the RaveSaber v1.0.0](https://github.com/Rave-Saber/Rave-Saber-Hardware/raw/master/img/schematic.png)


## Required Parts

* Breadboard
* Hookup Wire(24-22AWG)
* Atmel ATmega168A-PU Microchip
* 1x4 Male Header Pins(or make a cable to plug into the strip & breadboard
  using the hookup wire)
* Tactile Switch
* 144/m Dotstar LED Strip
* 5V Bench or DC Power Supply(you'll need ~8.7A for full brightness)

You'll also need an ISP programmer(like the [USBtinyISP][usbtinyisp]), some
wirestrippers, and maybe an ESD braclet or ESD-safe tweezers.

There is a Bill of Materials in `Mouser_BOM.xls` that you can use to import a
cart at [Mouser][mouser]. Simple go to `My Account` and choose `Import BOMs`
from the sidebar.


## Setup

![A Breadboard Drawing of the RaveSaber v1.0.0](https://github.com/Rave-Saber/Rave-Saber-Hardware/raw/master/img/breadboard.png)

1. Place the ATmega168a chip into the center of the breadboard.
1. Place the tactile switch and the male header pins.
1. Connect the ground & power buses to the microchip & header pins. If powering
   your chip from your ISP programmer, don't connect the chip to the power bus,
   but make sure the chip is connected to both the ground bus and programmer's
   ground pin.
1. Connect the switch to the chip & ground bus.
1. Connect the header pins to the chip.
1. Connect the ground pin from your power source to the ground bus, and then
   the positive end to the power bus.

Disconnect the power, connect your programmer, flash the [RaveSaber
Firmware][firmware], disconnect the programmer, & reconnect the power. You
should be able to long-press the button to illumunate the blade then
short-press to switch colors or long-press to power down the blade.


## TODO

* Schematics & PCB plans in KiCAD
* Voltage regulator circuits for running off batteries.
* Prototyping board layout
* Generate BOM: https://github.com/SchrodingersGat/KiBoM
    * Make sure to add DIP socket to BoM
* PCB w/ SMT components
* Link to upload gerbers to OSHPark: https://docs.oshpark.com/tips+tricks/api/
* Blade construction guide
* PVC Hilt construction guide
    * Eventually use MHS hilts as well, but that's not open hardware
    * See how much it'd cost to get someone to design an open/free hilt that
      machinists could reproduce.
* Recharge port

**Milestones**

v2.0.0 - prototype board w/ battery attached to some wood
v3.0.0 - pcb w/ pvc hilt & actual blade
v4.0.0 - pcb that fit MHS hilts

## References

**PVC Hilts**

* http://forums.thecustomsabershop.com/showthread.php?3266-Jay-gon-s-PVC-Hilts-Full-tutorial-on-last-page&p=138540&viewfull=1#post138540


## License

CERN OHL v1.2


[usbtinyisp]: https://learn.adafruit.com/usbtinyisp/overview
[mouser]: https://mouser.com
[firmware]: https://github.com/Rave-Saber/Rave-Saber-Firmware
