# OpenAmigaVideoHybrid
OpenAmigaVideoHybrid is an Open Hardware implementation of the Video Hybrid integrated circuit used in some Commodore Amiga computers.

![Board](https://raw.githubusercontent.com/SukkoPera/xxx/master/doc/render-top.png)

### Summary
The *Video Hybrid*, also known as *VIDIOT*, is a hybrid integrated circuit acting as a Digital-to-Analog Converter (DAC), which converts the digital 4-bit per color video signal of the Amiga into standard (analog) signals suitable to drive a monitor or TV.

It is used in the Amiga models A500, A500+, A600, A1000, A2000 and A3000. The Amiga 3000 actually uses two Vidiots: one for the 15kHz video output from Denise and one for the 31kHz video output from Amber.

### Architecture
The Video Hybrid has 5 sections, one for each of the red, green and blue colors, one for the synchronization signal and one for a composite monochrome signal.

The red, green and blue sections are identical: first, the digital signals are mixed using the typical *binary-weighted resistors* DAC configuration. After that, the level of the resulting signal is amplified through an NPN transistor. At the output, the signal is terminated at 75 ohms, as is typical for video signals.

The composite signal is generated in a similar way. The only significant differences are that the weighting resistors have different values and that the amplifier has two stages (NPN + PNP), in order to achieve a higher gain.

The synchronization signal is digital by nature, thus it needs no conversion, only some amplification.

### Components
It should now be clear that the Video Hybrid is not much more than a bunch of resistors and transistors, plus a few capacitors.

The original Video Hybrid uses a lot of resistance values which are rather odd by today's standards. While resistors with said values can still be found, they are becoming increasingly rarer and rather expensive.

Besides that, While the basic circuit has always remained the same, Commodore has used different values for some resistors in different revisions of the Video Hybrid. In particular, revision 3 uses higher resistance values in the synchronization signal section. Presumably, this was done to suppress crosstalk among the RGB channels (especially at 31kHz).

What this all means is that newer designs should suggest using different values that are readily available in the E24 series, which is common and cheap today, while maintaining functionality and performance.

The tables below lists the component values originally used by Commodore, along with some alternative values readily available in the E24 series.

|Resistors                             |390229-01/02|390229-03|E24   |
|--------------------------------------|------------|---------|------|
|R1, R9, R17, R25                      |1k          |1k       |1k    |
|R2, R10, R18                          |2k          |2k       |2k    |
|R3, R11, R19                          |4k          |4k       |3.9k**|
|R4, R12, R20                          |8k          |8k       |8.2k**|
|R5, R13, R21                          |470         |470      |470   |
|R6, R14, R22                          |390         |390      |390   |
|R7, R8, R15, R16, R23, R24, R29, R39\*|75          |75       |75    |
|R26                                   |220         |220      |220   |
|R27                                   |27k         |27k      |27k   |
|R28                                   |150         |150      |150   |
|R30\*                                 |18k         |90.9k    |91k   |
|R31\*                                 |7.5k        |37.4k    |62k   |
|R32\*                                 |2.7k        |13.3k    |22k   |
|R33\*                                 |1.2k        |6.04k    |10k   |
|R34\*                                 |7.5k        |37.4k    |62k   |
|R35\*                                 |3.9k        |19.6k    |20k   |
|R36\*                                 |120         |270      |220   |
|R37\*, R38\*                          |36          |36       |36    |

|Other Components                    |Value   |
|------------------------------------|--------|
|C1, C2, C3, C4, C5, C5\*            |100nF   |
|Q1, Q2, Q3, Q4, Q5\*                |MMBT3904|
|Q6\*                                |MMBT3906|

Notes:
- To achieve the highest video quality, it is strongly recommended to **use resistors with 1% tolerance** (or less) everywhere.
- Components marked with a single asterisk\* are only used by the circuit that generates the composite video signal. Since most of the original resistor values are uncommon, and since I don't think anybody really uses the composite output at all, I would just recommend not to mount these parts. If you really care for the (monochrome!) composite output, I wouldn't bother hunting down the correct parts and would just use the approximate values from the E24 series. They haven't been tested yet, but they should give a decent image that can still be used for whatever a monochrome output can be useful for (troubleshooting, I guess). Finally, note that all of these components (and only them!) have been grouped on the back side of the board for quick identification.
- On the contrary, values marked with two asterisks** are crucial for a precise and coherent conversion of color data from digital to analog, therefore it is recommended to stay as close as possible to the original values used by Commodore. Thus usage of 4.02k and 8.06k resistors (properly from the E96 series) is strongly encouraged (unless you can find resistors that are exactly 4k and 8k, of course). They will be slightly more expensive but the actual video quality will reward your choice.

### Installation
TBD

### Thanks
- The PCB layout was inspired by kipper2k's version of this board.
- This page contains a lot of content translated from [amigawiki](http://www.amigawiki.de/doku.php?id=de:parts:vidiot).
- [A good tutorial on DAC architectures](http://www.circuitstoday.com/digital-to-analog-converters-da) helped me to get a better understanding of DACs.
- [This](http://logwell.com/tech/components/resistor_values.html) helped me understand the rationale behind the actual resistor values available on the market.
