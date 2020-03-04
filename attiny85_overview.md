...

## NOTES ON MEMORY  
see datasheet, chapter 5.

2 main memory spaces, Data Memory and Program Memory. In addition, EEPROM for data storage (non volatile).

### 5.1 In System Reprogrammable Flash Program Memory  
tiny85 has 8kbytes of FLASH program memory.  
The program counter is a register that points to the instruction to be executed. it's 12 bits wide, to address 4096 program memory sections.  

### 5.2 SRAM Data Memory  
- first 32 locations are for the register file
- next 64 locations are for I/O registers
- last 512 locations are for internal data SRAM

addressing modes:  
 addressing modes for the Data memory cover: Direct, Indirect with Displacement, Indirect, Indirect with Pre-decrement, and Indirect with Post-increment  
 - direct addressing reaches all the space
 - indirect with displacement reaches 63 locations from the base address given by Y- or Z- registers. see more on register file, page 10.  
 
 #### 5.2.1 Access Time to data memory  
 - access to SRAM data memory is 2 clock cycles, one to compute address, the other to verify it's valid.
 
 ### 5.3 EEPROM data memory  
 512byte of EEPROM for ATtiny85.  
 access is done by specifying the EEPROM Address Registers, the EEPROM Data Register, and the EEPROM Control Register. For details see
“Serial Downloading” on page 151  
NOTE: it takes miliseconds to write/read to/from EEPROM, so that's not something I need now. it's used to save user settings, for example. 


