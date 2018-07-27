# CHANGELOG

## master

* Add power sub-circuit that uses a switching voltage regulator so the LEDs &
  microcontroller can run off of batteries.
* Add 10, 1, & 0.1 uF decoupling capacitors to the microcontroller's power &
  ground lines.
* Add a 16Mhz oscillator sub-circuit. This is only used if the
  microcontroller's fuses are set to use an external full-swing crystal.
* Add a reset button & pads for an external button.
* Add headers for programming & serial cables.
* Add KiCAD project for schematic.


## v1.0.0

The simplest way to start - connecting everything on a breadboard! This design
uses a tactile switch, headers for connecting the DotStar cable, and Atmel
ATmega168a microchip, and a 5V bench power supply.
