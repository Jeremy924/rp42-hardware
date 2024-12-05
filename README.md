# RP-42
The goal of RP-42 is to develop an affordable calculator that can run [Free42](https://github.com/Jeremy924/free42). The target cost for this was initially $20, but the final calculator costs slightly under $30. <br>
The calculator uses a STM32L475 microcontroller connected to a 8MB QSPI Flash. The operating system is stored on the STM32's internal 256KB Flash, while the Free42 application code is stored on the external flash drive. The QSPI interface can be memory mapped on the STM32, so the application code can be executed on the flash drive without copying to the RAM. 
<br>

## Development Timeline
07/06/2024 - Started designing PCB<br>
07/29/2024 - Completed PCB 0.0.4, and ordered PCB through JLCPCB<br>
08/04/2024 - Used Raspberry PI Zero 2W and ESP32-S3 to display Free42 on the LCD screen used in the calculator<br>
08/05/2024 - Began assemblying and testing<br>
08/11/2024 - STM32 communicates through micro USB port for the first time<br>
08/11/2024 - Test code is executed on the microcontroller, which showed that all the buttons and the LCD were working correctly. <br>
![image](https://github.com/user-attachments/assets/a73ca306-a018-498c-a43d-8846f27db169)
<br>
<i>In the test shown above, whenever a key is pressed, the number corresponding to the key that was pressed was displayed on the screen. The image shows that all the buttons were read correctly by the microcontroller.</i>
<br>The jumper wire in the image above is used to connect the UART RX pin to either GND or 3V. In the original PCB design, the BOOT0 pin on the STM32 was directly connected to 3V, however this did
not work because BOOT0 must be low in order to execute user code, even if the USB DFU is used to execute code. To correct this issue, the trace connected to the BOOT0 was broken, and the trace connected to the UART RX pin was broken. Becaues the traces were very close to each other, some solder was used to bridge the gap between the UART port and the BOOT0 pin. This way, the UART RX connector could be 
used to pull BOOT0 to low or high. 
<br><br>
08/21/2024 - STM32 can read and write to Flash drive through QSPI interface. <br>
08/21/2024 - Set up basic command line interface over USB VCP to make debugging easier, and created "frw" (flash read-write tool) to control flash. <br>
![image](https://github.com/user-attachments/assets/4bdc0d40-bb66-44ad-8ca9-dc76b7e29fa9)
<br><i>In the test shown above, thas flash read-write tool was used to write "Hello world" to the flash and then read it back. The test shows that the hardware and software for the flash is working correctly</i><br>

### Deadlines
12/08/2024 - Run Free42 on the calculator<br>
~~12/10/2024 - Complete 0.0.5 and order PCB <b>with SWD port</b>~~

## Schematics for 0.0.5
### Top Module
![image](https://github.com/user-attachments/assets/51828737-a401-4f4e-99ac-c00d169f923e)
### Keyboard
![image](https://github.com/user-attachments/assets/58d7577f-d4a1-400a-be3b-3f1d6bdd56fc)
### Screen
![image](https://github.com/user-attachments/assets/300fe28d-18eb-4225-9313-e00635356a56)
### MCU
![image](https://github.com/user-attachments/assets/82f5d69e-907a-4301-ace8-f6f22b73851a)
### Power Components
![image](https://github.com/user-attachments/assets/3dcc1c78-1fc3-4955-b7ae-99483c2f9150)
### PCB 0.0.5
![image](https://github.com/user-attachments/assets/ecac55cf-ab38-429f-ba24-589ba693ef6a)

## Hardware Changes for version 0.0.5
- [X] Add pad for battery terminal
      - temporary solution for 0.0.4: scrape off surface to access battery trace
- [X] Add button for BOOT0
      - temporary solution for 0.0.4: break current BOOT0 trace and connect it to backup RX trace. Then use RX connector to pull BOOT0 either high or low.
- [X] Add button for RES
      - temporary solution for 0.0.4: disconnect power.
- [X] **Add debug port**
- [X] move buttons closer together
- [X] connect VBAT to 3V rather than directly to battery. In its current state, if USB is connected and battery is not, then VBAT will be 0V, which is outside of recommended operating conditions.
- [X] move components further away from battery so that battery does not hit them if pushed in too far
- [X] add pull up resistor for external flash NCS pin so that it is pulled high while STM32 is booting.
- [X] add pull up resistor for on button so that mcu can be powered off and button will still be able to trigger interrupt

### Software Status
Currently, the software is able to control all of the components on the calculator. Additionally, the software is capable of connecting as a virtual com port and supports a basic command line interface.
The software is currently not ready to run Free42 yet. 
