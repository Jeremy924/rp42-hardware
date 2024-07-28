# Power Supplies
**VBAT** - 2.7V-3V: power directly from battery<br>
**GND**  - 0V<br>
**3V**   - 2.7V-3V: regulated voltage from USB/battery for mcu<br>
**3V PERPH** - 2.7V-3V: regulated voltage from USB/battery for peripherals<br>
**5V USB**    - 5V: power directly from USB<br>
**3V-5V**     - 2.7V-5V: unregulated power selected from USB if available or battery

# Nets:
### PWR_PERPH
Connections: *mcu* (pin 61/PB8, out), *U5* (PSU, in), R2(PSU,in)<br>
Enables power for the flash and the screen. <br>
Pulled down by a 100K resistor. The output from the mcu
can be in 3 states, high (enable peripherals),
high impedance (pulled low by resistor), or off (also pulled low by resistor).
The mcu pin should not be set to low could possibly be higher than 0V, which would
leak current.
### COL[0..5]
Connections: input_matrix (all buttons, out), mcu(pins 8-11,24,25/PC0-PC6, in)<br>
Pins are normally high impedance, so they should be pulled low by the mcu. If button is
pressed while mcu is scanning keyboard, then high output from ROW will pull the pin high.
### ROW[0..6]
Connections: input_matrix (all buttons, in), mcu(pins 13-20,31,43/PA0-PA4,PA8,PA10,out)<br>
Pins should normally be high impedance, except when scanning. When scanning, all pins should be 
low except for the pin that is currently being scanned. 
### ~RES
Connections: U1 (pin 39,in),mcu(pin 35/PB14,out)<br>
Used to reset the screen
### ~CS
Connections: U1 (pin 40,in),mcu(pin 34/PB13,out)<br>
Used to select the screen. This will probably always be low.
### ~A0
Connections: U1 (pin 38,in),mcu(pin 33/PB12,out)<br>
Used to select the address or data mode of the screen.
### SCL
Connections: U1 (pin 37,in),mcu(pin 51/PC10,out)<br>
Used to clock data into the screen.
### SI
Connections: U1 (pin 36,in),mcu(pin 53/PC12,out)<br>
Used to send data to the screen.
### D-
Connections: mcu (pin 44/PA11,io), CR1(pin 3,io)<br>
USB minus data. 
### D+
Connections: mcu (pin 45/PA12,io), CR1(pin 1,io)<br>
USB plus data.
### FLASH_IO[0..3]
Connections: mcu (pin 27/PB1,pin 26/PB0,pin 23/PA7,pin 22/PA6,io), U3(pin 5,2,3,7,io)<br>
Used to communicate with the flash chip.
### FLASH_NCS
Connections: mcu (pin 30/PB11,out), U3(pin 1,in)<br>
Used to select the flash chip.
### FLASH_CLK
Connections: mcu (pin 29/PB10,out), U3(pin 6,in)<br>
Used to clock data into the flash chip.
### D- IN
Connections: J1 (pin 2,io), CR1 (pin 4,io)<br>
USB minus data input. This is sent to the esd protection chip before 
going to the mcu.
### D+ IN
Connections: J1 (pin 3,io), CR1 (pin 6,io)<br>
USB plus data input. This is sent to the esd protection chip before
going to the mcu.