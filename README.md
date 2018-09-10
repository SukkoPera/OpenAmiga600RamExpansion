# OpenAmiga600RamExpansion
Open Hardware 1 MB Chip RAM Expansion for the Commodore Amiga 600 Computer

# WORK IN PROGRESS!

### Components
#### Connector
The female connector for the male edge connector on the A600 PCB is probably the hardest part to get hold of. Many people use PCI connectors, but they are longer and need to be trimmed. They are also hard to solder, most of the time. This project uses [a connector](https://coolcomponents.co.uk/products/edge-connector-for-bbc-micro-bit) that is normally used with the [micro:bit educational computer](http://microbit.org) instead. It was discovered by chance to be a perfect fit for the the A600, cheap and reliable.

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
|V53C16258HK35 |MOSEL VITELIC   |![Yes](doc/yes.png)|![Yes](doc/yes.png)  |[![PDF](doc/doc.png)](https://www.digchip.com/datasheets/parts/datasheet/308/V53C16258HK35-pdf.php)       |                                                                                     |
|V53C16258HK50 |MOSEL VITELIC   |![No](doc/no.png)  |                                                                                      |[![PDF](doc/doc.png)](https://www.digchip.com/datasheets/parts/datasheet/308/V53C16258HK50-pdf.php)       |                                                                                     |
|V53C16258SHK50|MOSEL VITELIC   |![Yes](doc/yes.png)|![Yes](doc/yes.png)  |[![PDF](doc/doc.png)](https://www.digchip.com/datasheets/parts/datasheet/308/V53C16258SHK50-pdf.php)      |                                                                                     |

Normally it is not necessary to mount all the decoupling capacitors. I usually skip C2 and C4. All of them are 100nF in the 0805 package anyway. An additional 10uF electrolytics capacitor can be mounted as C9, if needed. Might be a good idea if using a Vampire or a power hungry machine.

#### RTC
The entire RTC circuit is optional. It has been designed for an Epson [RTC62421](http://pdf.datasheetcatalog.com/datasheets/90/339927_DS.pdf) or [RTC72421](http://pdf.datasheetcatalog.com/datasheet/epson/RTC-72423.pdf), which don't need an external crystal nor any calibration. Both can be bought very cheaply from China; they will most likely be second-hand "pulls", but usually they will work fine.

The other components have some degree of flexibility:
- C7: 100 nF 0805 capacitor
- C8: >= 2.2 μF >= 10 V 1206 tantalum capacitor
- R1, R2, R3: 10K 0805 resistor
- R4, R5: 220-470 0805 resistor
- D1: BAT721C or BAT54C diode
- Battery Holder: Some cheap eBay one, usually called *BS-7*
- Battery: CR2032 3V Non-Rechargeable Lithium (a new one will last years)

Note that if you plan to store your Amiga or not to use it in a while, **you are recommended to remove the battery**. Failing to do this killed many A500+ computers and many A501 expansions in the past. The CR2032 battery used in this project is probably safer than the batteries used in those devices, but still I would not leave one in an unused Amiga. You have been warned.

### License
OpenAmiga600RamExpansion is Open Hardware. If you make any modifications to the board, please contribute them back.

### Get Support
If you need help or have questions, you can join [the official Telegram group](https://t.me/joinchat/HUHdWBC9J9JnYIrvTYfZmg).

### Thanks
- Thanks to the guys at the Italian Amiga Page forum, in particular:
  - fpmpaolo for suggesting the idea of making such a board
  - cpiace64 for providing me with a board to use as a template
  - majinga for helping with the testing
- The RTC circuit was copied shamelessly from the [Amiga 500 Expansion designed by PeteAU](http://eab.abime.net/showthread.php?t=85395) (which in turn probably copied it from Commodore).
- Footprint for [micro:bit edge connector](https://coolcomponents.co.uk/products/edge-connector-for-bbc-micro-bit) derived from work by [Anthony Kirby](https://github.com/anthonykirby/kicad_microbit_connector).
- Footprint for BS-7 Battery Holder taken from the [digikey-kicad-library](https://github.com/digikey/digikey-kicad-library).
