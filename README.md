# RaveSaber - AVR Hardware

This repository contains the hardware schematics, prototype board layout, parts
list, & setup guide for the RaveSaber electronics.

There is no blade or PCB design at the moment, but you can swing the LEDs
around using the prototype board & a piece of wood.


## Electronics Design

The Rave Saber board includes voltage regulation, utility headers, input
buttons, and an Atmel ATmega168a microchip.

### Connectors

![The various RaveSaber connectors](https://github.com/Rave-Saber/Rave-Saber-Hardware/raw/master/img/schematic-connectors.png)

`J1` is where power enters the board from the battery. We use JST connectors
for our battery wiring. The battery power is fed through the power sub-circuit
to get a regulated voltage of 5V.

`J2` is where the Dotstar strips connect to the board. The data & clock signals
come from the microchip while the power connections come from the power
circuit.

`J3` & `J4` are optional connectors that ease programming & development. `J3`
is a FTDI Serial connection that can be used to preview/sample different colors
with our [color testing firmware][color-test]. `J4` is an ISP connector that
allows you to re-program the microchip without having to pull it out of it's
socket.

### Power

![The RaveSaber voltage regulation circuit](https://github.com/Rave-Saber/Rave-Saber-Hardware/raw/master/img/schematic-power.png)

The power circuit uses a LM2576TV-5G switching voltage regulator to step down
the battery voltage to 5V. It can pump out a maximum of 3 Amps, which is used
to power the microcontroller & the LEDs.

The circuit design is derived from the voltage regulator's datasheet. `C1` &
`C2` should be low-ESR capacitors rated for at least 16V(with a minimum ESR of
50 milliOhms for `C2`). `C2` can be anywhere from 1000 to 2000 uF. `L1` must be
an inductor rated for at least 3 amps, going slightly over that is encouraged.
`D1` should be rated for 20V.

### Microcontroller

![The RaveSaber microcontroller connections](https://github.com/Rave-Saber/Rave-Saber-Hardware/raw/master/img/schematic-microcontroller.png)

The microcontroller circuit is mostly just connections to the other circuits.

Bypass capacitors are used on the connection to the power circuit. `C3` & `C4`
are optional but `C5`, the 100nF capacitor, should always be included. The
analog reference & power pins are connected to the power supply even though
they are not used - this is recommended in the ATmega datasheet.

### Crystal Oscillator

![The RaveSaber oscillator circuit](https://github.com/Rave-Saber/Rave-Saber-Hardware/raw/master/img/schematic-oscillator.png)

The oscillator circuit is pretty fluid. You can use a different frequency
crystal(with a maximum of 20Mhz), or leave out the entire circuit and use the
ATmega's 8Mhz internal oscillator instead. If you do modify the circuit, make
sure your microcontroller's fuses are correctly programmed for your desired
clock source and change the definition of the `F_CPU` macro in the firmware's
`Makefile` to your new frequency.

### Button

![The RaveSaber button circuits](https://github.com/Rave-Saber/Rave-Saber-Hardware/raw/master/img/schematic-buttons.png)

The main button is `SW1`. It is used to ignite/extinguish the saber & cycle
through the programmed patterns. We've included both a tactile switch for
development and an external connection so you can put your board in a hilt.

The reset button, `SW2`, is optional but ocassionally useful for testing &
development.


## Required Materials

### Equipment

You'll want to have the following equipment/supplies:

* 22AWG Solid Hookup Wire
* AVR Programmer(like the [USBtinyISP][usbtinyisp])
* Wire Strippers
* Flush Cutters
* Soldering Iron & Solder
* PCB Holder(optional)
* Anti-static Bracelet or ESD-safe Tweezers(optional)

If you're only testing this out on a breadboard you can get away with just:

* Breadboard
* Wire & Strippers
* AVR Programmer
* 5V Power Supply

### Components

For the breadboard, you just need an ATmega168a microcontroller & a tactile
button.

For the prototyping board, you will need the following:


| Part | Description | Link |
|---|---|---|
| | 22x27 through-hole prototyping board | [Amazon][protoboard] |
| BAT | 7.4v Li-Ion battery | [TCSS][battery] |
| LED | DotStart Strip, 144/m | [Mouser][led-strip] |
| J1 | 2-pin JST connector | [TCSS][jst-connector] |
| J2 | 4-pin, 2.54mm pitch male header | [Amazon][headers] |
| J3 | 6-pin, 2.54mm pitch male header | [Amazon][headers] |
| J4 | 2x3-pin, 2.54mm pitch male header | [Amazon][headers] |
| C1 | 100uF low-ESR electrolytic capacitor | [Mouser][100-cap] |
| C2 | 1000-2000uF low-ESR electrolytic capacitor | [Mouser][1200-cap] |
| C3 | 10uF capacitor | [Amazon(assorted)][elec-cap-kit] |
| C4 | 1uF capacitor | [Amazon(assorted)][elec-cap-kit] |
| C5 | 100nF capacitor | [Amazon(assorted)][cer-cap-kit] |
| C6, C7 | 20pF capacitor | [Mouser][20-cap] |
| D1 | 3A, 20V Schottky Diode | [Mouser][diode] |
| L1 | 47uH, 3A Fixed Inductor | [Mouser][inductor] |
| Y1 | 16Mhz Crystal | [Mouser][crystal] |
| SW1, SW2 | 6mm SPST OFF-(ON) tactile switch | [Mouser][switch] |
| U1 | LM2576TV-5G - 5V, 3A switching voltage regulator | [Mouser][vreg] |
| U2 | 28-pin DIP IC socket | [Amazon][dip-socket] |
| U2 | Atmel ATmega168A-PU - AVR microcontroller | [Mouser][atmega] |

[protoboard]: https://amzn.to/2L2IWVJ
[battery]: http://www.thecustomsabershop.com/74v-Li-ion-2600mAh-18650-Battery-Pack-P699.aspx
[led-strip]: https://www.mouser.com/ProductDetail/485-2242
[jst-connector]: http://www.thecustomsabershop.com/JST-connector-kit-male-and-female--P941.aspx
[headers]: https://amzn.to/2Mx6HtK
[100-cap]: https://www.mouser.com/ProductDetail/710-870135675003
[1200-cap]: https://www.mouser.com/ProductDetail/667-EEU-FC1A122S
[elec-cap-kit]: https://amzn.to/2wb0Ekk
[cer-cap-kit]: https://amzn.to/2PiyX1K
[20-cap]: https://www.mouser.com/ProductDetail/594-S200K25SL0N63L6R
[diode]: https://www.mouser.com/ProductDetail/863-1N5820G
[inductor]: https://www.mouser.com/ProductDetail/673-PE-53112NL
[crystal]: https://www.mouser.com/ProductDetail/520-HCA1600-20X
[switch]: https://www.mouser.com/ProductDetail/506-FSM4JH
[vreg]: https://www.mouser.com/ProductDetail/863-LM2576TV-5G
[dip-socket]: https://amzn.to/2Mo4dOU
[atmega]: https://www.mouser.com/ProductDetail/556-ATMEGA168A-PU


## Setup

### Breadboard

A breadboard can be used for simple testing of colors/patterns as well as
flashing the microchip with new firmware. You could use a smaller breadboard
for the saber instead of a prototyping board, but it's not nearly as durable.
Be wary of drawing too much current through your breadboard - you might melt
it! Initial attempts used batteries and voltage regulation with the breadboard,
but these instructions will assume you are running everything off a 5V bench
power supply.

1. Place the ATmega168a chip in the center of the breadboard.
1. Connect the switch to ground and pin 4(PD2/INT0) of the microchip.
1. Connect pin 19(SCK) to the Dotstar strip's clock pin & pin 17(MOSI) to the
   strip's data pin.
1. Connect your power supply's 5V & ground leads to the microchip & Dotstar
   strip.

You should now be able to connect the GND, SCK, MOSI, MISO, & RESET pins of
your programmer and flash your chip with the [RaveSaber Firmware][firmware].
Leave the VCC pin on your programmer unconnected since power is coming from
your bench supply.

### Prototyping Board

A prototyping board is the recommended way to setup v2.0.0 of the RaveSaber
hardware.

![The Prototyping Board Layout of the RaveSaber v2.0.0](https://github.com/Rave-Saber/Rave-Saber-Hardware/raw/master/img/prototyping-board.png)

The prototyping board is assembled by placing components and bridging pads with
component leads, solder bridges, & wire. We've ommited `C4`, the 1uF decoupling
capacitor but feel free to add it in.

First we place the components and make what connections we can with the
component leads:

1. Start by placing the capacitors on the board and bending the leads so they
   stay on the board when you flip it over. You can also tack them into place
   with a small amount of solder.
1. Place the switches and voltage regulator. These should fit tight enough that
   they don't fall out when you flip the board over. If they do, tack them into
   place with some solder on the pins.
1. Place the DIP socket for `U2` and tack it into place by soldering some of
   the unused pins.
1. Connect `C1` and `U1` by bending the leads of `C1` and soldering them together.
1. Bridge `GND` & `ON/OFF` of `U1` together. This keeps the regulator always
   running.
1. Place and solder `L1`. Bend & solder the positive lead of `C2` to connect
   the two.
1. Since the leads of `D1` are too thick for the board's holes, bend them down
   the board and solder each one over multiple pads.
1. Connect and solder the negative leads of `C2`, `C3`, `C5`, & `SW2`. Do the
   same with the positive leads of `C3` & `C5`.
1. Use spare lead cuttings to bridge all the ground pins of `SW1` & `SW2`
   together. Bridge the top pins of each switch together as well, keeping the
   tops of `SW1` & `SW2` unconnected.
1. Place & solder `Y1`. Use the right leads of `C6` & `C7` to connect & solder
   them to the crystal and then to the proper DIP-socket pins.
1. Place and solder the `J2`, `J3`, & `J4` headers. Use just enough solder to
   get them to hold into place - it'll make their wire connections easier to
   solder.
1. Bridge the ground pins of the serial & LED headers together. Leave space for
   the ground wire between `C2` and the LED header.

Everything should now be on the board & the remaining connections can be made
with your 22-gauge wire. We did this in the following order:

1. `U1` to `L1`, `D1`, & `C2`.
1. `C3` positive lead to `C2`.
1. `C5` to VCC & GND of `U2`.
1. `U2` second GND(pin 22) to `SW1`.
1. `RESET` from `U2` to `SW2`.
1. `BTN` from `U2` to `SW1`.
1. `TXD` from `U2` to `RXD` of the serial header, followed by `RXD` to `TXD`.
1. `RESET` from `U2` to the ISP header.
1. `C2` to VCC & GND of the LED header.
1. `GND` from `C2` to `C6`, `C7`, & the ISP header.
1. `MOSI` & `SCK` from `U2` to the LED header.
1. `MOSI`, `MISO`, `SCK` from `U2` to the LED header.
1. Connect two wires to `C1` and terminate them with the JST connector.

Everything should be connected, your circuit should resemble the schematics, &
your prototyping board should resemble the above layout.

Place the ATmega168a into the DIP socket at `U2` & connect the Dotstar strip,
your Programmer's ISP cable, and the battery. Flash the [RaveSaber
Firmware][firmware] & disconnect the programmer.

You should now be able to long-press the button to illumunate the blade then
short-press to switch patterns or long-press again to power down the blade.


## TODO

* Add model number to Components table
* PCB w/ SMT components using KiCAD
* Auto-generate BOM: https://github.com/SchrodingersGat/KiBoM
    * Make sure to add DIP socket to BoM
* Link to upload gerbers to OSHPark: https://docs.oshpark.com/tips+tricks/api/
* Blade construction guide, using TCSS blade parts
* PVC Hilt construction guide
    * Eventually use MHS hilts as well, but that's not open hardware
    * See how much it'd cost to get someone to design an open/free metal hilt
      that machinists could reproduce.
* Recharge port

**Future Milestones**

v2.0.0 - prototype board w/ battery attached to some wood

v3.0.0 - pcb w/ pvc hilt & actual blade

v4.0.0 - pcb that fit MHS hilts


## References

**Hilts**

* [Jay-gon's PVC Hilt Tutorial](http://forums.thecustomsabershop.com/showthread.php?3266-Jay-gon-s-PVC-Hilts-Full-tutorial-on-last-page&p=138540&viewfull=1#post138540)

**Blades**

* [Neopixel Blade Assembly - FX-Sabers](https://www.fx-sabers.com/forum/index.php?PHPSESSID=06jl1sddsstpq4hvnu0c9fat74&topic=51357.0)
* [LED Blade Assembly](https://www.youtube.com/watch?v=Qbl4K-v4G_s)


## License

CERN OHL v1.2


[color-test]: https://github.com/Rave-Saber/AVR-APA102-Color-Tester
[usbtinyisp]: https://learn.adafruit.com/usbtinyisp/overview
[mouser]: https://mouser.com
[firmware]: https://github.com/Rave-Saber/Rave-Saber-Firmware
