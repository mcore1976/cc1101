
Simple packet radio on ATMEGA328p (arduino) and CC1101 chip.  
Allows bidirectional communication from PC/smartphone(when USB to Serial used) to PC/smartphone.
The code is based on PANSTAMP library adopted by  Panagiotis Karagiannis for pure AVR-GCC. Hex file to be uploaded directly to ATMEGA328P via USBASP programmer.

You can see how it works here : https://www.youtube.com/watch?v=4cPxHEn-Uqc


To upload program code to the chip using cheapest USBASP programmer (less than 2 USD on eBay/Aliexpress) look at this page : http://www.learningaboutelectronics.com/Articles/Program-AVR-chip-using-a-USBASP-with-10-pin-cable.php

Link to video how to program the chip : https://www.youtube.com/watch?v=7klgyNzZ2TI

-------------------------------------------------------------------------------------------------------------------------------

LINUX PC :


The script attached in repository ( "compileatmega"  ) can be used to upload data to the chip if you have Linux machine with with following packages : "avr-gcc", "avr-libc" and "avrdude". For example in Ubuntu download these packages using command : "sudo apt-get install avr-gcc" , "sudo apt-get install avr-libc", "sudo apt-get install avrdude" and you are ready to go.

-----------------------------------------------------------------------------------------------------------------------------

WINDOWS PC :

If you have Windows 10 machine - follow this tutorial to download and install full AVR-GCC environment : http://fab.cba.mit.edu/classes/863.16/doc/projects/ftsmin/windows_avr.html and use "compileatmegaXX.bat" files for compilaton in the directory where you have downloaded mainX.c files. You have to be logged as Windows Administrator and run "cmd" from search window to do that. Then use commands like "cd XXXXX" to change working directory to get to downloaded source files.

----------------------------------------------------------------------------------------------------------------------------

HARDWARE DETAILS :

Current settings of the devices are : Radio 38400 bps,  operating frequerncy 433MHz, 9600baud on serial port PC, 10mW of Power.
If you want different setting you need to use SmartRF application from Texas Instruments to generate the settings for CC1101 chip registers : http://www.ti.com/tool/SMARTRFTM-STUDIO

CC1101 breadboard operates on 3.3V power and 3.3V TTL logic. For this reason when 5V VCC power is taken from USB (like in the prototype the power is taken directly from USB pin) to drop down the voltage 3x 1N4007 diodes are connected in serial. 

The design can be simplified. The quartz crystal (XTAL + 2x 22pF capacitors) is NOT necessary if you don't want to have stable serial port clock frequency. The compilation script can select internal 8MHz RC Oscilator (put E2 hex value as a fusebit). 
Anyway to achieve 100% synchro with all RS232 serial port speeds  a proper crystal is required (3.6864 MHz) - there is "main2.c" code optimized for such XTAL 3.6864 MHz 

The device requires FTDI232 USB to serial converter (operating on 3,3V logic) - or any other USB to Serial 3.3V converter -  to interface ATMEGA328P with PC (PUTTY for the PC or FTDI Serial Terminal on Android).
PUTTY terminal must be configured for 9600 bps, 8N1, no flowcontrol check

In the code I am using ATMEGA328P interrupt from Serial UART ( to receive ASCII from Serial Port of PC) and interrupt from INT0 pin ( which is connected to GDO0 on CC1101 breadboard) which is generated when data transmitted/received over CC1101 radio.

After fine tuning of CC1101 radio options - by enabling :
a) 2-FSK modulation 
b) lowering Radio speed to 1200 baud 
c) frame size 32 bytes, 
d) deviation +-5.2k
- you can achieve communication range up to several kilometers even with 10mW radio power.


Have fun !
