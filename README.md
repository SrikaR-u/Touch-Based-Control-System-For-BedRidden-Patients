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

https://github.com/jjHF47t/TOUCH-BASED-DEVICE-CONTROL-SYSTEM-FOR-BEDRIDDEN-PATIENTS-#features
   


