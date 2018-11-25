
Simple packet radio on ATMEGA328p (arduino) and CC1101 chip.  Allows bidirectional communication from PC/smartphone(when USB to Serial used) to PC/smartphone.
The code is based on PANSTAMP library adopted by  Panagiotis Karagiannis for pure AVR-GCC. Hex file to be uploaded directly to ATMEGA328P via USBASP programmer.

Current settings of the devices are : Radio 38400 bps,  operating frequerncy 433MHz, 9600baud on serial port PC, 10mW of Power.
If you want different setting you need to use SmartRF application from Texas Instruments to generate the settings for CC1101 chip registers : http://www.ti.com/tool/SMARTRFTM-STUDIO

CC1101 breadboard operates on 3.3V power and 3.3V TTL logic. For this reason when 5V VCC power is taken from USB (like in the prototype the power is taken directly from USB pin) to drop down the voltage 3x 1N4007 diodes are connected in serial. 

The design can be simpler. The quartz crystal (XTAL + 2x 22pF capacitors) is NOT necessary. The compilation script can select internal 8MHz RC Oscilator (put E2 hex value as a fusebit). Anyway to achieve 100% synchro with 115200 and other serial port speeds  a proper crystal is required (11.0592 MHz) but you have to recalculate "delay" function using the page : http://www.bretmulvey.com/avrdelay.html

The device requires FTDI232 USB to serial converter (operating on 3,3V logic) - or any other USB to Serial 3.3V converter -  to interface ATMEGA328P with PC (PUTTY for the PC or FTDI Serial Terminal on Android).
PUTTY terminal must be configured for 9600 bps, 8N1, no flowcontrol check

In the code I am using ATMEGA328P interrupt from Serial UART ( to receive ASCII from Serial Port of PC) and interrupt from INT0 pin ( which is connected to GDO0 on CC1101 breadboard) which is generated when data transmitted/received over CC1101 radio.



You can see how it works here : https://www.youtube.com/watch?v=4cPxHEn-Uqc

Have fun !
