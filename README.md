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

## ✨ Key Features

* **Secure Password Authentication:** Access control via 4x4 matrix keypad input validated against non-volatile storage.
* **EEPROM Persistence:** Non-volatile SPI EEPROM storage for user passwords with real-time update functionality.
* **Intuitive Touch Control:** Coordinate-mapped touch screen interface enabled upon successful login.
* **Dual Appliance Control:**
  * **Device 1:** Light Control (LED1)
  * **Device 2:** Fan Control (LED2)
* **Emergency Panic System:** One-touch emergency buzzer activation for patient assistance.
* **Real-Time Status Monitoring:** 16x2 LCD display provides visual feedback on device status and system prompts.
* **Interrupt-Driven Architecture:** Asynchronous UART interrupt handling for responsive touch data processing.

---

## ⚙️ System Architecture & Working Principle

1. **Initialization:** System boots and initializes LCD, UART, SPI, GPIO matrix keypad, EEPROM, and interrupt vectors.
2. **Authentication:**
   * Microcontroller reads the saved password from the **AT25LC512 SPI EEPROM**.
   * User inputs a security code via the **4x4 Matrix Keypad**.
   * Code is verified against EEPROM memory.
3. **Control Mode Enabled:**
   * Touch screen monitoring activates via **UART Interrupts**.
   * User interacts with designated touch zones to toggle **LED1 (Light)**, **LED2 (Fan)**, or trigger the **Emergency Buzzer**.
   * Password can be updated securely at any time and saved to EEPROM.
4. **Visual Feedback:** All state changes and interaction logs are instantly mirrored to the **16x2 LCD Display**.

---

## 🛠️ Hardware Architecture

| Hardware Component | Specification / Function | Interfacing Protocol |
| :--- | :--- | :--- |
| **Microcontroller** | LPC2148 (ARM7TDMI-S 32-bit MCU) | System Core |
| **Touch Screen** | Resistive Touch Screen Module | UART (Interrupt Driven) |
| **EEPROM** | AT25LC512 (512 Kb) | SPI Communication |
| **Keypad** | 4x4 Matrix Keypad | GPIO Matrix Scanning |
| **Display** | 16x2 Character LCD | GPIO (4-bit/8-bit Parallel) |
| **Actuators** | LEDs (Light & Fan) & Buzzer | GPIO Digital Output |
| **Power Unit** | Regulated 3.3V / 5V DC Power Supply | Power Distribution |

---

## 💻 Software Architecture & Stack

* **Programming Language:** Embedded C
* **Integrated Development Environment (IDE):** Keil µVision4 / µVision5
* **Flash Programming Tool:** Flash Magic
* **Simulation Environment:** Proteus Design Suite (Optional)

---

## 🧩 Peripheral Modules

* **`LCD Interface`**: Displays authentication status, operational modes, and real-time device states.
* **`Keypad Interface`**: Scans button presses for password entry and system configuration.
* **`UART Module`**: Intercepts raw touch screen coordinates using UART RX interrupts (`UART0`/`UART1`).
* **`SPI EEPROM Module`**: Handles byte/page read and write cycles over SPI bus lines (MOSI, MISO, SCK, CS).
* **`Touch Processing Module`**: Translates analog $X, Y$ coordinate frames into discrete control zones.
* **`Device Control Module`**: Toggles digital output pins for appliance relays/LEDs and audio alarm drivers.

## 🏥 Applications
* **Smart Hospital Rooms: Accessible bedside device operation for bedridden patients.
* **Elderly Care & Assistive Living: Enhanced independence for senior citizens.
* **Rehabilitation Centers: Aids patients recovering from motor function loss.
* **Home Automation Systems: Accessible control interface for general household devices.
  
## 🔮 Future Enhancements
* [ ] IoT Integration: Add ESP8266/ESP32 module for web and mobile application dashboards.
* [ ] Wireless Connectivity: Integrate Bluetooth (HC-05) / Wi-Fi for remote caregiver alerts.
* [ ] Cloud Telemetry: Push activity logs and emergency timestamps securely to the cloud.
* [ ] Vital Signs Monitoring: Add pulse oximetry ($SpO_2$), heart rate, and body temperature sensor arrays.
* [ ] Multi-Relay Expansion: Expand driver circuits to control higher-load AC appliances (TV, Air Conditioner, adjustable beds).
  
## 🏆 Project Outcomes
* Successfully engineered a secure, micro-controlled assistive interface on LPC2148.
* Implemented reliable non-volatile password verification over SPI EEPROM.
* Handled real-time touch coordinate inputs asynchronously using UART interrupts.
* Developed modular drivers in Embedded C for bare-metal hardware orchestration.

## 📄 Conclusion
* The Touch-Based Device Control System provides a safe, reliable, and user-friendly interface tailored for patient care.
* By combining hardware-level security (EEPROM) with responsive interrupt programming, this project forms a solid, production-ready blueprint for next-generation assistive medical devices and smart room automation.
   


