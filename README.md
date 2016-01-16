Particle Spark/Photon to WeMos Adapter
======================================

This adapter is used to put in place of a Spark/Photon a WeMos board with ESP8266 I needed for a specific French [project][3]. I needed SPI for RFM69 Module with IRQ on ~~GPIO2~~ GPIO15 and SS on GPIO2 (see below why).
I choosed ~~NodeMCU~~ WeMos boards instead of ESP8266 because they have all I need on board, such as pullups, switches, USB power, 3/3V regulator, USB2Serial... You can find more information on WeMos [site][1] that is really well documented.
WeMos board are now used instead of NodeMCU's one because they're just smaller, features remains the same, but I also suspect WeMos regulator far better quality than the one used on NodeMCU that are just fake of originals AMS117 3V3.

Since ESP8266 has less pin than Particle boards, only "classic" have been connected

- SPI Interface (GPIO12 to 14) GPIO15 is used for RFM69 IRQ
- I2C Interface (GPIO14 and GPIO5)
- Serial (GPIO1 and GPIO3)
- GPIO0 as free I/O (Flash button on NodeMCU)
- GPIO2 is used as Chip Select (SS) for RFM69
- GPIO16 as free I/O (LED and KEY on NodeMCU)

To boot correctly ESP8266 needs some pins at defined level, GPIO15 must be LOW and GPIO2 must be HIGH. Unfortunatlly with RFM69 connected as IRQ to GPIO2 and SS to GPIO15 it does not boot because RF69 pull it DIO IRQ to LOW, making GPIO2 LOW and ESP8266 not booting. The fix is to reverse the wiring, connect IRQ to GPIO15 and SS to GPIO2 (and do according changes in the code). 
- Teleinfo had some issue due to NodeMCU USB/Serial onboard converter that was in conflict and was killing RX signal coming from optocoupler. To avoid this I've put 2 inverters to have a correct RX Teleinfo signal coming to EMP8266. No Risk because on board RX Signal of WeMos has a 470 Ohm resistor in serial of this line. To avoid this may be we could use a ESP8266 without any USB/Serial adapteur such as a Adafruit [Huzzah][5], Olimex [ESP8266 Dev][6] or even [OAK][6]
- to be able to handle all Remora PCB version I added the feature to enable/disable Téléinfo FET Staging (they will already be placed on Remora V1.3 PCB) using Jumper J1 & J2.

*Boards are ordered as testing from OSHPark, I did not fully tested them yet, I will update as soon has I got them in my hands. Use at your own risks*

Detailed Description
====================

Look at the schematics for more informations.

### Schematic  
![schematic](https://raw.githubusercontent.com/hallard/Particle2WeMos/master/Particle2WeMos-sch.png)  

### Boards  
<img src="https://raw.githubusercontent.com/hallard/Particle2WeMos/master/Particle2WeMos-top.png" alt="Top" width="40%" height="40%">&nbsp;
<img src="https://raw.githubusercontent.com/hallard/Particle2WeMos/master/Particle2WeMos-bot.png" alt="Bottom" width="40%" height="40%">&nbsp; 


You can order the PCB of this board v1.0 at [OSHPARK][4]

### Assembled boards

I'm currently waiting for boards from OSHPARK


##License

You can do whatever you like with this design.

##Misc
See news and other projects on my [blog][2] 
 
[1]: http://www.wemos.cc/wiki/doku.php?id=en:d1_mini
[2]: https://hallard.me
[3]: https://github.com/thibdct/programmateur-fil-pilote-wifi/tree/master/Logiciel/remora
[4]: https://oshpark.com/shared_projects/rnk2lmmh
[5]: https://www.adafruit.com/product/2471
[6]: https://www.olimex.com/Products/IoT/MOD-WIFI-ESP8266-DEV/
[7]: http://digistump.com/products/145

