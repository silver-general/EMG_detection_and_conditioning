I have found a couple of ways to do that. Some are high level (meaning: you can see fewer things during the process), others force you to look at the makefile and modify things manually and can be more instructive. 

### WAYS OF PROGRAMMING (I'll copy my onenote notes here soon)
-- NOTE: so far I managed to compile C files. I still have to try do that in assembly.

- arduino IDE
- Atmel Studio, calling avrdude as external tool
- winavr

## Physical connection
to program the microcontroller using arduino, you must connect the ports: MOSI,MISO,SCK,RESET,Vcc,GND

## Programming a microcontroller overview

In System Programming (ISP) is used to upload instructions to the ATtiny85 microcontroller unit (MCU). beforse uploading the instruction, though, some fuses settings have to be applied. those are the MCU clock (can be downscaled from 8MHz to 1MHz), EEPROM erase disabler, and such. NOTE: you can disable RESET in fuses. this is bad, you can't reprogram the MCU later! this is done as a parameter in avrdude in the computer terminal.

In general, the steps are:

- create an executable file (compile a C file, Assembly file, as .hex)
- upload on the MCU using avr dude tool. avr dude takes parameters determining stuff like fuse settings ("what the MCU clock should be?", "can the EEPROM be erased?", and so on) and whereto the executable should be written or read or verified (eg: written on FLASH)  
- for a list of avrdude parameters: https://www.ladyada.net/learn/avr/avrdude.html
- for the fuse settings: http://www.engbedded.com/fusecalc/


## ATMEL STUDIO
I followed this, but some part of it is wrong, so just understand the basic flow https://www.instructables.com/id/Integrate-ArduinoISP-and-Atmel-Studio/

Atmel Studio can detect automatically the most common AVR programmers, but not Arduino used as a programmer. to do that, you need to use avrdude as an external tool.

- tool->custom tool-> command: address of avrdude; arguments: fuses settings.
- the example uses ```-U lfuse:w:0xe6:m -U hfuse:w:0xd9:m -e -v -patmega328p -carduino -PCOM2 -b19200 -D -Uflash:w:"$(ProjectDir)Debug\$(ItemFileName).hex":i -C"C:\Program Files (x86)\Arduino\hardware\tools\avr\etc\avrdude.conf"```  
I had to change some parameters for my atmega2560 programming the attiny85:
-- part number: -p ATtiy85  
-- COM port of the arduino: PCOM6 (see in your computer device manager)  
-- path where avrdud.conf is located (look into the arduino installation folder)  
-- fuses settings: see  http://www.engbedded.com/fusecalc/  
-- command to write to FLASH and the hex file address. use TargetName instead of ItemFileName. (NOTE: check the output files in Avr Studio. there's a difference between  "build filename" (returns the output file filename.hex) and "build solution" (return gccapplication.hex, so it's not the name you want!)
-- I deleted -D (disable chip erase). why should I keep it? it did not allow a new program to be uploaded.

therefore, something like this should be launched as avrdude parameter:	-v -v -v -p  ATtiny85 -c arduino -P COM6 -b 19200 -U flash:w:"$(TargetDir)$(TargetName).hex":i -C "C:\Program Files (x86)\Arduino\hardware\tools\avr\etc\avrdude.conf" -U lfuse:w:0x62:m -U hfuse:w:0xdf:m -U efuse:w:0xff:m  
* -v -v -v : super verbose
* -p ATtiny85 : part number is the MCU you are programming
* -c Arduino : programmer you are using. it's the arduino
* -P COM6 : the port arduino is connected to
* -b baudrate 19200 : default baudrate, should be the speed of communication. I need to study mode on this)
*  flash:w:"$(TargetDir)$(TargetName).hex":i this writes "w" on "flash" a ".hex" file. Atmel Studio uses that syntax to point to the program location.
* -C "C:\Program Files (x86)\Arduino\hardware\tools\avr\etc\avrdude.conf" : path to avrdude.config. note the quotes, because "Program File" has a space in the name. windows is lame.
* -U lfuse:w:0x62:m -U hfuse:w:0xdf:m -U efuse:w:0xff:m : fuses settings. these are the default. 

### Atmel Studio Theory  
read the documentation.  
this is the way atmel studio builds the project and in the solution explorer window some files appear.
	1. EEP file: EEPROM content
	2. ELF file: everything written on the device, including fuses
	3. HEX: flash content
	4. LSS: disassembled ELF file. this is the assembly file!
	5. MAP file: Linker info, what it did and decided
	6. SREC file: HEX but in motorola format(I will learn more?)


## method 2: AVR toolchain
https://www.instructables.com/id/Getting-Started-With-WinAVR/

more on this later.

## method 3 Arduino IDE  
note: I have to verify this again.  
this was the least instructive way because tutorials make you miss all the juicy stuff about resetting fuses, AVR libraries used, and the steps of program compilation, and what the heck avrdude does with his parameters.

- Download the tiny libraries in arduino IDE
- Upload the sketch "arduino isp" in the atmega. this makes it a programmer 
- Select programmer: "Arduino as ISP"  
- Set ATtiny clock to 1 MHz downscale (it's the default value)
- other settings: defaults should be ok
- get an example, like a blink. define pins according to atmega, or leave default (pin 5 should blink)
- upload with "sketch -> upload using programmer" OR "upload" after applying a 10microfahrad capacitor between RESET and GND of atmega

## method 4 (linux):
...

