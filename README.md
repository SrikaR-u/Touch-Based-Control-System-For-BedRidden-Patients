# Touch-Based-Control-System-For-BedRidden-Patients

A secure, embedded Password-Protected Touch-Based Device Control System designed to assist individuals with limited mobility or bedridden patients. The system leverages an ARM7 microcontroller, a serial resistive touch screen, a matrix keypad, and an SPI EEPROM to safely operate essential appliances and trigger emergency alerts with minimal physical effort.

🛠️ Hardware Architecture:
The project is built around the LPC2148 (ARM7TDMI-S) microcontroller, interfacing with the following peripherals:  Microcontroller: LPC2148  Touch Input: Sunrom 1255 Resistive Touch Screen Controller (Serial interface at 9600 bps)  Security Input: 4x4 Matrix Keypad (for password authentication and modification)  Storage: Microchip 25LC512 512 Kbit SPI Serial EEPROM (for non-volatile password storage)  Display: 16x2 Character LCD (System status, coordinates, and password prompt)  Outputs & Indicators:Device 1 & 2: Dedicated LEDs acting as appliance relays  Buzzer: Emergency patient alert system  LCD Power Control: Power-saving/blink toggle option.

Block Diagram:
 <img width="927" height="566" alt="image" src="https://github.com/user-attachments/assets/e99f7516-3a55-41c3-abe2-b84c67411cf5" />


  
⚙️ Memory & Peripheral:
Specifications:

1.Serial Touch Controller Data Format (Sunrom 1255)The module streams a fixed 22-byte ASCII packet at 9600 bps containing 4-digit filtered X, Y coordinate maps and a Z (pressure) value:  Start Frame: 0x0A (Line Feed)  Data Payload Format: X:0065 Y:0089 Z:0029  End Frame: 0x0D (Carriage Return) 

2. SPI EEPROM (25LC512)Operating Voltage: Must run at 3.3V when paired with LPC2148.  Memory Depth: 512 Kbits (65,536 bytes) arranged with a 128-byte page buffer.  Function: Stores the secure master unlock password.
   

 🚀 Application Firmware Logic:
 The system follows a state machine topology controlled via peripheral validation layers:  Authentication Phase: The system boots and prompts for a master password via the 16x2 LCD. The entered key is compared against the valid credential block pulled from the 25LC512 EEPROM.  Activation Phase: If authenticated, the system exposes the Touch Panel command processing routine.  Control Matrix Phase: Touch coordinates map directly to peripheral driver sets:  Top Left Space ($X < 300, Y < 300$): Energizes LED1 / Device 1.  Top Right Space ($X > 700, Y < 300$): Energizes LED2 / Device 2.  Bottom Left Space ($X < 300, Y > 700$): Trips the Emergency Alert Buzzer.  Center Matrix Layer ($400 < X < 600, 400 < Y < 600$): Toggles / blinks the LCD backlight rail. 
 
 Credential Modification Phase: When an external hardware interrupt is asserted via the Interrupt Switch (I.SW), the system enters configuration mode, updating the secure space on the EEPROM with a revised password sequence. 

 🛠️ Setup & Compilation Pipeline:
 PrerequisitesIDE- Keil uVision (ARM7 Compiler Toolchain)  Flash Utility: Flash Magic tool  Hardware Line Couplers: USB-to-UART bridge / MAX232 transceiver circuit for touch screen PC debugging logs.
 
 Execution Framework:
 Clone this repository to your build environment.  Open Keil uVision, configure target hardware architecture parameters using a standard LPC2148 profile engine.Add projectmain.c alongside associated driver configuration files.Compile your binaries to generate the executable production .hex code.Couple the target controller dev board to your platform layout using serial lines, initialize Flash Magic, select your target .hex file, and flash the software to the system target.  

