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
   

 Features
Password-protected system access
EEPROM-based password storage
Password validation using keypad input
Password update and EEPROM write functionality
Touch-screen based device control
Device1 (LED1) ON/OFF control
Device2 (LED2) ON/OFF control
Emergency buzzer activation
LCD status monitoring
UART interrupt-based touch data reception
SPI communication with EEPROM
Secure and user-friendly operation
Hardware Requirements
LPC2148 ARM7 Microcontroller
Resistive Touch Screen Module
16x2 LCD Display
4x4 Matrix Keypad
AT25LC512 SPI EEPROM
LED1 (Light Control)
LED2 (Fan Control)
Buzzer
Power Supply
Software Requirements
Embedded C
Keil µVision IDE
Flash Magic
Proteus (Optional)
Working Principle
System initializes LCD, UART, SPI, Keypad, EEPROM, and Interrupt modules.

Stored password is read from EEPROM.

User enters a password through the keypad.

Password is validated against EEPROM data.

If authentication is successful:

Touch screen control is enabled.
Device1 (LED1) can be switched ON/OFF.
Device2 (LED2) can be switched ON/OFF.
Emergency buzzer can be activated.
Touch control can be disabled when not required.
Password can be modified securely.

Updated password is saved permanently in EEPROM.

LCD continuously displays device status and user feedback.

Modules Used
LCD Interface
Displays authentication messages, device status, and user instructions.

Keypad Interface
Used for password entry and password modification.

UART Communication
Receives touch-screen coordinate data through interrupt-driven communication.

SPI EEPROM Interface
Stores and retrieves user passwords securely.

Touch Screen Interface
Processes touch coordinates and maps them to control actions.

Interrupt Handling
Handles touch-screen communication and password update operations efficiently.

Device Control Module
Controls LEDs and buzzer based on touch-screen input.

Applications
Smart Hospital Rooms
Bedridden Patient Assistance Systems
Elderly Care Systems
Assistive Healthcare Devices
Smart Home Automation
Rehabilitation Support Systems
Future Enhancements
IoT Integration: Enable remote monitoring and control of devices through a mobile app or web dashboard.
Wi-Fi/Bluetooth Connectivity: Allow wireless communication with caregivers and healthcare staff.
Cloud-Based Data Storage: Store patient activity and alert logs securely in the cloud.
Patient Health Monitoring: Integrate sensors for heart rate, body temperature, SpO₂, and blood pressure monitoring.
Multiple Device Control: Expand the system to control additional appliances such as fans, lights, TVs, and medical equipment.
Technologies Used
Embedded C
LPC2148 ARM7
UART Communication
SPI Protocol
EEPROM Interfacing
LCD Interfacing
Keypad Interfacing
Touch Screen Interfacing
Interrupt Programming
Project Outcomes
Developed a secure touch-based control system using LPC2148.
Implemented password authentication with EEPROM storage.
Integrated LCD, Keypad, EEPROM, Touch Screen, UART, and SPI modules.
Designed interrupt-driven communication for efficient operation.
Enabled independent device control for patients with limited mobility.
Improved understanding of embedded system design and peripheral interfacing.
Created a modular and scalable embedded application.
Conclusion
The Touch-Based Device Control System for Bedridden Patients successfully provides a secure and accessible method for controlling devices using a touch interface. By integrating password authentication, EEPROM storage, UART communication, SPI interfacing, and interrupt-driven control, the system enhances patient independence and safety. The project serves as a strong foundation for future healthcare automation and smart assistive technologies.

About
Password-Protected Touch-Based Device Control System for Bedridden Patients using LPC2148. The system enables patients to control devices through a resistive touchscreen after password authentication. EEPROM stores passwords securely, while LEDs and a buzzer provide device control and emergency alerts for safe, independent operation.

Resources
Readme
Activity
Stars
0 stars
Watchers
0 watching
Forks
0 forks
Report repository
Releases
No releases published
Packages
No packages published
Contributors
1
 (1)
@jjHF47t
jjHF47tSampth Kumar
Languages
C
100%
Footer


