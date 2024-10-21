# RP42
The primary goal of this project is to develop an affordable calculator that can run Free42. The target cost for this was initially $20, but the final calculator costs slightly under $30. <br>
The calculator is based on the STM32l475 microcontroller, which has 256KB of internal flash, and 128KB of SRAM. Because 256KB is not enough storage for Free42, an external 8MB flash drive is connected through QSPI.
<br>
<br>
## RP42 0.0.4-b
0.0.4-b is the first version of RP42 that was made into a PCB. 

### Hardware Status
There are some hardware bugs that were discovered while testing the PCB, but the hardware is still fully functional. 

[RP42 Front Image](https://github.com/Jeremy924/rp42-hardware/blob/main/docs/img/altuim-3d-front.png)

Hardware Changes
- [ ] Add pad for battery terminal
      - temporary solution: scrape off surface to access battery trace
- [X] Add button for BOOT0
      - temporary solution: break current BOOT0 trace and connect it to backup RX trace. Then use RX connector to pull BOOT0 either high or low.
- [X] Add button for RES
      - temporary solution: disconnect power.
- [ ] **Add debug port**
- [ ] move buttons closer together
- [X] connect VBAT to 3V rather than directly to battery. In its current state, if USB is connected and battery is not, then VBAT will be 0V, which is outside of recommended operating conditions.
- [ ] move components further away from battery so that battery does not hit them if pushed in too far
- [X] add pull up resistor for external flash NCS pin so that it is pulled high while STM32 is booting.
- [X] add pull up resistor for on button so that mcu can be powered off and button will still be able to trigger interrupt

### Software Status
Currently, the software is able to control all of the components on the calculator. Additionally, the software is capable of connecting as a virtual com port and supports a basic terminal system.
The software is currently not ready to run Free42 yet. 
