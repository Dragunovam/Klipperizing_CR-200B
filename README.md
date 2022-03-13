# CR-200B_Klipper

This will become a detailed guide to modify the CR-200B into a klipper printer. The CR-200B is very capable out of the box, but lacks basic settings like z-offset and many other tuning capabilities. Even though open source Marlin firmware binaries have been made to remedy these shortcomings, klipper has a larger community and support.

Unfortunately this printer is not very well documented. I was glad to at least find a few sources on the internet, I will give the due credit on the bottom of this guide.

## Klipper host

Due to the current (2022) shortage of raspberry pi's, I have chosen use a creality wifi box. Raspberry pi zero could be used for this project, but most users will not be comfortable working with the PSU and GPIO on the creality mainboard.  These tiny machines have two fully working USB ports and have enough computing power to act as klipper host. The option exists to run two klipper host instances on one box, this way one box can actually connect with two klipper printers at the same time. The two reserved USB ports can be used to either run two printer, or run one printer and one webcam for remote monitoring (more about that later!).
