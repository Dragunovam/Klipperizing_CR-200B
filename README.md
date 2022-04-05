![afbeelding](https://user-images.githubusercontent.com/20616914/158082022-752270ed-cef6-4291-854c-35b0ab6ffe26.png)


# CR-200B_Klipper

This will become a detailed guide to modify the CR-200B into a klipper printer. The CR-200B is very capable out of the box, but lacks basic settings like z-offset and many other tuning capabilities. Even though open source Marlin firmware binaries have been made to remedy these shortcomings, klipper has a larger community and support.

Unfortunately this printer is not very well documented. I was glad to at least find a few sources on the internet, I will give the due credit on the bottom of this guide.

## Klipper host

![afbeelding](https://user-images.githubusercontent.com/20616914/158082090-cadaf019-1a10-4462-b8a8-d2cb9f7c9cbc.png)


Due to the current (2022) shortage of raspberry pi's, I have chosen to use a creality wifi box. Raspberry pi zero could be used for this project, but most users will not be comfortable working with the PSU and GPIO on the creality mainboard.  These tiny machines have two fully working USB ports and have enough computing power to act as klipper host. The option exists to run two klipper host instances on one box, this way one box can actually connect with two klipper printers at the same time. The two reserved USB ports can be used to either run two printers, or run one printer and one webcam for remote monitoring (more about that later!).


## UART mode for the stepper drivers

Most creality (silent) motherboards come with pretty capable drivers. Unfortunately their capabilities are not fully utilized and they are locked in standalone (stealthchop) mode. There is nothing inherently wrong with this mode, it is actually preferable if noise is a concern. However there are a few problems with stealthchop. Linear advance (Marlin) and the analogous pressure advance (klipper) on the extruder driver are not possible in stealthchop mode. Excessive oozing and better nozzle pressure control are factors that can drastically change the quality at a much higher printing speeds. Some other issues are aslo the lack of vref/amperage tuning. To better tune the CR-200B's VREFS, the motherboard offers a few pots that can be turned with a screwdriver. This is a very cumbersome process and it is inferior compared to the alternative, a fine-grained digital controll of control of the stepper frequencies that completely bypass the voltage pots.

To liberate the full capabilities of the CR-200B we can simply connect a few resistors/IO's to put the stepper drivers in single-wire UART mode.
My printer came with a 4.2.5 board, it seems that the A on the SD-card reader indicates they contain TMC2208 drivers. Some lucky devils might have three TMC2208 drivers for each axis and one TMC2209 for the extruder. Some even luckier devils might even have four TMC2209 drivers for the three axes and the extruder. In My setup, I choose to equip the printer with a CR-Touch leveling probe. This is practically the same as the BL-Touch probe, the klipper configuration should be the same. On some cloned bltouch probes it's very important to change a few parameters in the klipper config file, klipper has issues getting the clones to work properly without a few important config changes. The bed springs on most creality printers are not very stiff and this contributes to the inability to properly level the bed. Upgrading them to solid metal or silicone blocks is a good idea. Even with better springs, the bed has enough overhang to bend the whole front downwards. This messes up the geometry of the final print and in my opinion it makes the use of a sensing probe mandatory.

By Adding the sensing probe, the Z-endstop on top of the printer is no longer necessary. I reccommend to unplug the cable from the endstop itself, it's not necassary to remove the cable on the motherboard. One additional step is to remove the endstop screw on the printing bed. If you don't remove the screw (wich is screwed in pretty deep, good luck getting it out in one breath) the screw might end up smashing against the z-endstop. These endstops are not expensive to replace, but the torque of the stepper is enough to smash the endstop end its mounting holes on the printer.

### After removal the endstop screw comes out with a spring along its shaft. The z-endstop is simply disabled by unplugging the cable.
![z-endstop and endstop screw](https://user-images.githubusercontent.com/20616914/161829822-e1d0537e-df85-47f6-b7ab-90986407f791.jpg)
