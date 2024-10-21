**A Pico ATX and Pi Pico Power Supply and Scan Converter for the Macintosh 128/512/Plus**

A board to power a Macintosh 128/512/Plus from a Pico ATX PSU, as well as to generate a VGA video signal from an onboard Pico scan converter.
This board was designed inconjunction with the Sony SND Replacement to support my work on the Macintosh Plus clone.

![PicoABBoardFront](https://github.com/user-attachments/assets/419713a1-d29e-4005-930a-13e1a480d75a)

**So, What Is It?**

This is a combined power supply and VGA scan converter for a Macintosh 128/512 or Plus.
The VGA scan converter is based off the work by the GuruThree:
https://github.com/guruthree/mac-se-video-converter

The firmware for the Pico is available within that repository.
The hardware for the VGA scan converter is based off of the VGA reference design as provided here:
https://datasheets.raspberrypi.com/rp2040/hardware-design-with-rp2040.pdf

The PSU portion of the deisgn is intended to be used with a Pico PSU, although any suitable ATX PSU can be used. 
The connector is identical to that of the Macintosh 128/512/Plus, so either a Molex KK396 11 way connector can be installed with an appropriate cable,
or the board can be soldered directly to the Macintosh Logic Board.
 
VDEV1 units have been assembled and worked first time. No modifications to the board were necessary at all. Additionally, I have built an equivalent system using a Pimoroni VGA board (as per the original repository) and with a Pico ATX PSU.


![photo_2024-08-20 21 39 24](https://github.com/user-attachments/assets/88271ef8-4a55-4f9a-b27b-e36976ec2192)


**Additional Features**

Aside from providing Power and a VGA signal from the Logic board, it also has some additional features:

1) Option for Composite Video with associated jumper -  the scan converter can be compiled to generate a PAL video signal from the red channel,
as such, there is an RCA connector with a jumper to select whether the required output.
Please note that the firmware will need to be recompiled with the PAL video option, and the video signal is known to be quite poor.
It's something to be fixed at some point.

2) Pads for -5v and -12V, as well as a -5v regulator - the regulator and pads are provided in case the user is intending to use the Sony SND replacement
(https://github.com/DosFox1/Sony-SND-THT-Replacement/tree/main), or if a board is installed that requires off board -5v to be regulated (such as an SE)
In normal operation, the -5v regulator and pads are not needed, and can be DNF'd (Do Not Fit).

3) Optional potential divider - the original scan converter does call for the use of a standard voltage level shifter, it was found that the 128/512/Plus appear to output
a signal that was lower than what the level shifter expected, resulting in the system not working. Further investigation reveals that the output from the board is in the region
of 3.8v - which is in the limits of a V1 Pico, as well as V2 Pico (which are 5v tolerant). Regardless, current limiting resistors have been added, and if so desired, additional resistors can be added (or diodes!) for added protection. This is a VDEV1 design, so extra protection may be added for the next iteration. Your mileage may vary!

5) Speaker pin header - the speaker output is routed to a separate pin header, to make it easier to add an external speaker.

6) RTC diodes and battery option - two diodes have been added, as well as an additional header to add a 4.5v battery pack for the RTC.
I would suggest ensuring that the battery pack is stored well away from the logic board and the analogue board, to avoid battery leakage.

7) Power Supply Switch with pads - external power switch with pads has been added, allowing the user to install either a switch at the rear of the unit, or to add an external toggle switch to power the system on, if so desired.

8) Onboard Power LED and external pads - onboard power LED is provided to prove that the 5v rail has powered up. Also the option to mount an LED elsewhere within the case if so desired.


**Part List**

Much like the Sony SND, the parts are relatively easy to source, although there may be some difficulty finding the precision value resistors. 
The parts are as follows:

<pre>
Part     Value            Device                       Package                 Library             Sheet

C1       100n 50V         100N_TH_CAP                  CAP_5.08MM_PITCH        Capacitors TH       1
C2       100n 50V         100N_TH_CAP                  CAP_5.08MM_PITCH        Capacitors TH       1
CN1      V06-1x20-SV-GF-1 PICO_BOARD                   PICO_SOCKET             uProcessor          1
CN2      2way             PIN_HEADER_2W_VERT_TH        2W_2.54MM_PITCH_VERT_TH Connectors          1
CN3      2way             PIN_HEADER_2W_VERT_TH        2W_2.54MM_PITCH_VERT_TH Connectors          1
CN4      V06-1x3-SV-GF-1  PIN_HEADER_3W_VERT_FEMALE_TH 3W_2.54MM_PITCH_VERT_TH Connectors          1
CN5      2way             PIN_HEADER_2W_VERT_TH        2W_2.54MM_PITCH_VERT_TH Connectors          1
CN6      2way             PIN_HEADER_2W_VERT_TH        2W_2.54MM_PITCH_VERT_TH Connectors          1
CN7      DB15             DB15                         DB15                    SparkFun-Retired    1
CN8      ATX24RH          ATX24RH                      ATX24_RIGHT_ANGLE       SparkFun-Connectors 1
CN9      RCA              RCA                          RCA                     SparkFun-Connectors 1
CN10     11 Way KK        KK-156-11                    KK-156-11               con-molex           1
D1       1N4004           1N4004                       DO41-10                 adafruit            1
D2       1N4004           1N4004                       DO41-10                 adafruit            1
LED1     Red              5MM_LED_RED                  5MM_TH_VERT_STANDARD    Optoelectronics     1
R1       470R             470R_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R2       47R              47R_TH_RESISTOR              RESISTORTHRUHOLE        Resistors TH        1
R3       47R              47R_TH_RESISTOR              RESISTORTHRUHOLE        Resistors TH        1
R4       1k               1K_TH_RESISTOR               RESISTORTHRUHOLE        Resistors TH        1
R5       2k               2K_TH_RESISTOR               RESISTORTHRUHOLE        Resistors TH        1
R6       4k02             4K02_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R7       8k06             8K06_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R8       499R             499R_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R9       1k               1K_TH_RESISTOR               RESISTORTHRUHOLE        Resistors TH        1
R10      2k               2K_TH_RESISTOR               RESISTORTHRUHOLE        Resistors TH        1
R11      4k02             4K02_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R12      8k06             8K06_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R13      499R             499R_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R14      1k               1K_TH_RESISTOR               RESISTORTHRUHOLE        Resistors TH        1
R15      2k               2K_TH_RESISTOR               RESISTORTHRUHOLE        Resistors TH        1
R16      4k02             4K02_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R17      8k06             8K06_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R18      499R             499R_TH_RESISTOR             RESISTORTHRUHOLE        Resistors TH        1
R19      22R              22R_TH_RESISTOR              RESISTORTHRUHOLE        Resistors TH        1
R20      22R              22R_TH_RESISTOR              RESISTORTHRUHOLE        Resistors TH        1
R21      22R              22R_TH_RESISTOR              RESISTORTHRUHOLE        Resistors TH        1
R22      DNF              22R_TH_RESISTOR              RESISTORTHRUHOLE        Resistors TH        1
R23      DNF              22R_TH_RESISTOR              RESISTORTHRUHOLE        Resistors TH        1
R24      DNF              22R_TH_RESISTOR              RESISTORTHRUHOLE        Resistors TH        1
SP1      1PIN             1PIN                         1PIN                    generic parts       1
SP2      1PIN             1PIN                         1PIN                    generic parts       1
SW1      SS12D16-GDN5     SS12D16-GDN5                 THRUHOLE90DEGSLIDESW    Switches            1
VREG1                     7905T                        TO220H                  linear              1
</pre>

**Notes on Assembly**

The board has been designed so anyone with a decent amount of soldering experience should be able to assemble one. 
The PCBs themselves can be ordered from your favourite PCB fab house, mine have been ordered from JLCPCB (sorry PCBWay).
Owing to the fact that the board is a relatively simple two layer design, the boards shouldn't be too expensive.
The cost of my boards came to $2 for five, but should usually be $4 for five PCBs - regardless - they are cheap!
The firmware that generates a VGA signal and targets a standard V1 Pico (RP2040 based) has been added to this repository. 
Pico2 (RP2354) and PAL video versions will be added eventually. Current firmware now fixes an annoying issue where the video output
was distinctly yellow - this has now been fixed.
For assembling into cases, SVGs of the board have been added - just import the board edge file to your favourite SVG editor to start designing a case for it!
