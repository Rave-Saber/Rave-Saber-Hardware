# CHANGELOG

## master

* Fix machine-pin component for `J2` and component/footprint mismatch for `J3`.
  The previous `J2` component we linked to had pin diameters much too small to
  hook up to the DotStar strip. The previous `J3` component had the solder pad
  for pin 1 on the right side of the footprint instead of the left side.  To
  address this, we link to a 20-pin strip with proper pin widths & break them
  into the sizes & orientations necessary.
* Move Jumper & Switch silkscreen labels to outside their footprints.
* Switch the 0603 Capacitor footprints to a slightly more elongated version.
* Shift the footprint of SW2 up so that it's courtyard does not
  intersect with J4's.
* Ensure L1 silkscreen does not intersect with solder pads.
* Fix footprint size of C2 by creating a new custom footprint.


## v3.0.0

This version upgrades the prototyping board & through-hole components to a
printable PCB design & SMD components. We've also bumped the oscillator crystal
to 20Mhz to squeeze as much power out of the microcontroller as possible.

* Add KiCAD PCB schematic with SMD components.


## v2.0.0

This is actually a portable version that you can swing around. The electronics
are constructed on a prototyping board so they are much more secure than the
breadboard, and a voltage regulator has been added so we can run off of
rechargable 7.4V Li-Ion batteries.

There is still no blade or hilt design though - swinging this around means
attaching the LED & electronics to a piece of wood.

* Document the electronics circuit design.
* Add an example layout for a prototyping board along with a list of required
  components and a build guide.
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
