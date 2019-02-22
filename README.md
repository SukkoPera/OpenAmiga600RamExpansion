# OpenAmiga600RamExpansion
OpenAmiga600RamExpansion is an Open Hardware 1 MB Chip RAM Expansion for the Commodore Amiga 600 Computer with optional Real Time Clock.

![Board](https://raw.githubusercontent.com/SukkoPera/OpenAmiga600RamExpansion/master/doc/render-top.png)

### Summary
The Amiga 600 computer by Commodore originally came with 1 MB of Chip RAM. Like all "compact" Amiga models, it has a trapdoor in the bottom, through which a memory expansion can be installed, bringing the chip RAM to a maximum of 2 MB.

Back in the day, some expansions also came with a Real-Time Clock (RTC), which allowed the Amiga to keep track of the current date and time, which is most useful if you use AmigaDOS a lot. While this was mostly ordinary for Amiga 500 expansions, it was not so common on those for the Amiga 600, and even most expansions designed today do not bear an RTC circuit.

OpenAmiga600RamExpansion is an Open Hardware implementation of such an expansion, including the RTC.

### Components
#### Connector
The female connector for the male edge connector on the A600 PCB is probably the hardest part to get hold of. Many people use PCI connectors, which have the correct pitch but are longer and need to be trimmed. They are also hard to solder, most of the time. This project uses [a connector](https://coolcomponents.co.uk/products/edge-connector-for-bbc-micro-bit) that is normally used with the [micro:bit educational computer](http://microbit.org) instead. It was discovered by chance to be a perfect fit for the the A600, cheap and reliable.

#### Memory
The required RAM Type is 4 Mbit (256k×16) DRAM in the SOJ-40 package with up to 70-80 ns access time, e.g.:

|Model         |Maker           |Tested                                                                              |Working                                                                               |Data Sheet                                                                                                                                                                 |Notes                                                                                |
|--------------|----------------|:----------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|-------------------------------------------------------------------------------------|
|AS4C256K16E0  |Alliance        |![No](doc/no.png)  |                                                                                      |[![PDF](doc/doc.png)](http://www.dexsilicium.com/Alliance_AS4C256K16E0.pdf)                               |                                                                                     |
|HM514260AJ8   |Hitachi         |![No](doc/no.png)  |                                                                                      |                                                                                                                                                                           |                                                                                     |
|HM514260JP8   |Hitachi         |![No](doc/no.png)  |                                                                                      |                                                                                                                                                                           |                                                                                     |
|HY514260BJC   |Hyundai         |![No](doc/no.png)  |                                                                                      |                                                                                                                                                                           |                                                                                     |
|KM416C256BJ   |Samsung         |![No](doc/no.png)  |                                                                                      |                                                                                                                                                                           |                                                                                     |
|IC41C16257-35K|ICSI            |![No](doc/no.png)  |                                                                                      |[![PDF](doc/doc.png)](http://pdf.datasheetcatalog.com/datasheet2/f/0x3d8ida5x0jift9qq8jrfp8adpy.pdf)      |IF this works, _-S_ version should work, too. Do NOT use _LV_ versions.              |
|µPD424260     |NEC             |![No](doc/no.png)  |                                                                                      |                                                                                                                                                                           |                                                                                     |
|V53C16256HK50 |MOSEL VITELIC   |![Yes](doc/yes.png)|![Yes](doc/yes.png)  |[![PDF](doc/doc.png)](https://www.digchip.com/datasheets/parts/datasheet/308/V53C16256HK50-pdf.php)       |                                                                                     |
|V53C16258HK30/35/50 |MOSEL VITELIC   |![Yes](doc/yes.png)|![Yes](doc/yes.png)  |[![PDF](doc/doc.png)](https://www.digchip.com/datasheets/parts/datasheet/308/V53C16258HK35-pdf.php)       |                                                                                     |
|V53C16258SHK50|MOSEL VITELIC   |![Yes](doc/yes.png)|![Yes](doc/yes.png)  |[![PDF](doc/doc.png)](https://www.digchip.com/datasheets/parts/datasheet/308/V53C16258SHK50-pdf.php)      |                                                                                     |

Most of these chips can be found on eBay or on AliExpress very cheaply (i.e.: 1-2€ each).

Normally it is not necessary to mount all the decoupling capacitors. I usually skip C2 and C4. All of them are 100nF in the 0805 package anyway. An additional 10uF electrolytic capacitor can be mounted at C9, if needed. Might be a good idea if using a *Vampire* board or a power-hungry machine.

RAM chips can either be soldered directly on the board or installed in sockets. While soldering the chips might not be trivial for the unexperienced, sockets for the SOJ-40 package are quite expensive and not really easier to solder either, so the choice is up to you.

#### RTC
The entire RTC circuit is optional. It has been designed for an Epson [RTC62421](http://pdf.datasheetcatalog.com/datasheets/90/339927_DS.pdf) or [RTC72421](http://pdf.datasheetcatalog.com/datasheet/epson/RTC-72423.pdf), which don't need an external crystal nor any calibration. Both can be bought very cheaply from China: they will most likely be second-hand "pulls", but usually they will work fine.

The other components have some degree of flexibility:
- C7: 100 nF 0805 capacitor
- C8: >= 2.2 μF >= 10 V 1206 tantalum capacitor
- R1, R2, R3: 10K 0805 resistor
- R4, R5: 220-470 0805 resistor
- D1: BAT721C or BAT54C diode
- Battery Holder: Some cheap eBay one, usually called *BS-7*
- Battery: CR2032 3V Non-Rechargeable Lithium (a new one will last years)

Note that if you plan to shelve your Amiga or not to use it for a while, **you are recommended to remove the RTC battery**. Failing to do so killed many A500+ computers and many A501 expansions in the past. The CR2032 battery used in this project is probably safer than the barrel batteries used in those devices, but still I would not leave one in an unused Amiga. You have been warned.

### Installation
After everything has been soldered, just open the trapdoor on your Amiga, install the expansion (the correct orientation is with the chips closer to the keyboard) and put the cover back on.

I recommend to run [SysTest](https://github.com/keirf/Amiga-Stuff) then. Use the Memory option (<kbd>F1</kbd>), it must show 2 MB of Chip RAM. Then start the Memory Test (<kbd>F1</kbd> again) and let it run for 50-100 rounds: if it doesn't find any errors, you are probably good to go.

SysTest also has an option for reading and resetting the RTC (<kbd>F7</kbd> then <kbd>F3</kbd>), so try that as well. If you are using SysTest >= 1.2 you can also set the date and time with it, otherwise you will have to use other tools (Workbench is a good candidate).

### License
OpenAmiga600RamExpansion is Open Hardware. If you make any modifications to the board, please contribute them back.

### Disclaimer
OpenAmiga600RamExpansion is provided to you 'as is' and without any express or implied warranties whatsoever with respect to its functionality, operability or use, including, without limitation, any implied warranties of merchantability, fitness for a particular purpose or infringement. We expressly disclaim any liability whatsoever for any direct, indirect, consequential, incidental or special damages, including, without limitation, lost revenues, lost profits, losses resulting from business interruption or loss of data, regardless of the form of action or legal theory under which the liability may be asserted, even if advised of the possibility or likelihood of such damages.

### Support the Project
Since the project is open you are free to get the PCBs made by your preferred manufacturer, however in case you want to support the development, you can order them from PCBWay through this link:

[![PCB from PCBWay](https://www.pcbway.com/project/img/images/frompcbway.png)](https://www.pcbway.com/project/shareproject/OpenAmiga600RamExpansion_V1.html)

You get my gratitude and cheap, professionally-made and good quality PCBs, I get some credit that will help with this and [other projects](https://www.pcbway.com/project/member/shareproject/?bmbid=41100). You won't even have to worry about the various PCB options, it's all pre-configured for you!

Also, if you still have to register to that site, [you can use this link](https://www.pcbway.com/setinvite.aspx?inviteid=41100) to get some bonus initial credit (and yield me some more).

Again, if you want to use another manufacturer, feel free to, don't feel obligated :).

### Get Help
If you need help or have questions, you can join [the official Telegram group](https://t.me/joinchat/HUHdWBC9J9JnYIrvTYfZmg).

### Thanks
- Thanks to the guys at the Italian Amiga Page forum, in particular:
  - fpmpaolo for suggesting the idea of making such a board
  - cpiace64 for providing me with a board to use as a template
  - majinga for helping with the testing
- The RTC circuit was copied shamelessly from the [Amiga 500 Expansion designed by PeteAU](http://eab.abime.net/showthread.php?t=85395) (which in turn probably copied it from Commodore).
- Footprint for [micro:bit edge connector](https://coolcomponents.co.uk/products/edge-connector-for-bbc-micro-bit) derived from work by [Anthony Kirby](https://github.com/anthonykirby/kicad_microbit_connector).
- Footprint for BS-7 Battery Holder taken from the [digikey-kicad-library](https://github.com/digikey/digikey-kicad-library).
