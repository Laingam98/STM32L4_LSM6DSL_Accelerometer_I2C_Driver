# 🚀 STM32L4S5I: LSM6DSL 6-Axis IMU Driver (I2C & EXTI)

This repository features a robust, bare-metal-style **Embedded C driver** for the onboard **LSM6DSL 6-Axis IMU**, leveraging the STM32L4S5I IoT Discovery Kit (STBL4S5I). The project focuses on precise I2C data acquisition for the accelerometer and utilizes the **External Interrupt (EXTI)** line for efficient sensor-ready signaling, demonstrating key embedded systems design principles.

---

## 💡 Project Architecture & Value

This project showcases core competencies essential for an Embedded Systems Engineer:

| Strategic Focus          | Technical Achievement Demonstrated                                                                                                         |
| :----------------------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| **Sensor Interfacing** | Developed reliable **I2C Master** communication to initialize the LSM6DSL sensor, read its WHO_AM_I register, and acquire raw sensor data. |
| **Efficient Design** | Configured and utilized the **GPIO EXTI Interrupt** (Pin PD11) to allow the sensor to signal the MCU when new data is ready, minimizing CPU polling and demonstrating proficiency in asynchronous event handling. |
| **STM32 Toolchain** | Comprehensive peripheral configuration (I2C, UART, GPIO, NVIC) and code generation using **STM32CubeIDE** for the STM32L4S5I microcontroller. |
| **Data Processing** | Implemented logic to read raw 16-bit accelerometer data and prepare it for transmission via UART.                                           |

---

## 📖 User Manual

This guide provides the necessary steps to configure the hardware, set up the software environment, deploy the code, and verify the functionality.

### 1. Objective 🎯

To interface the onboard LSM6DSL motion sensor with the STM32L4S5I microcontroller, read the 3-axis accelerometer data via I2C, and transmit the values over UART for real-time monitoring.

### 2. Hardware Requirements 🛠️

* **Board:** STMicroelectronics STBL4S5I IoT Discovery Kit (The LSM6DSL sensor is integrated).
* **Cable:** Micro-USB cable (Type-A to Micro-B).

### 3. Software Requirements 💻

* **IDE:** **STM32CubeIDE** (Version 1.10.0 or later recommended).
* **Packs:** Ensure the necessary **STM32Cube MCU & Firmware Packs** for the STM32L4 series are installed within CubeIDE. The **X-CUBE-MEMS1** pack is essential for LSM6DSL support files and examples.
* **Terminal:** A Serial Terminal Emulator (e.g., Tera Term, PuTTY, RealTerm, or the built-in terminal in STM32CubeIDE).

### 4. Hardware Setup 🔌

1.  **Connect Board:** Connect the STBL4S5I board to your PC using the Micro-USB cable plugged into the **STLINK USB connector (CN1)**. This provides power, debug/programming, and the Virtual COM Port.

### 5. Software Configuration (STM32CubeIDE) ⚙️

This project requires specific peripheral settings configured via the `.ioc` file in STM32CubeIDE. Key configurations include:

1.  **Middleware/Packs:**
    * Enable **X-CUBE-MEMS1**.
    * Select **Device MEMS1\_Applications -> Board Part AccGyr - LSM6DSL - I2C**.

 <img width="842" height="212" alt="1" src="https://github.com/user-attachments/assets/318c2c57-59a0-442f-91ac-7c5ed1795e8e" /> <img width="688" height="183" alt="2" src="https://github.com/user-attachments/assets/f87ecda7-5def-42c2-b7ce-1ba450f6669c" />


2.  **I2C Configuration:**
    * Enable **I2C2** (Mode: `I2C`, Speed: `Fast Mode`).
    * Assign pins: `PB10` -> `I2C2_SCL`, `PB11` -> `I2C2_SDA`.
      
      
<img width="1507" height="700" alt="4" src="https://github.com/user-attachments/assets/4170fb6b-7a89-402b-ab2d-d8b7f51054b8" /> 



3.  **UART Configuration:**
    * Enable **USART1** (Mode: `Asynchronous`).
    * Assign pins: `PB6` -> `USART1_RX`, `PB7` -> `USART1_TX`.
    * Set Baud Rate to `115200`.

<img width="1527" height="707" alt="3" src="https://github.com/user-attachments/assets/431ebec3-9c00-4ea7-8bd8-3cb7e7acf2d6" />

      
4.  **Interrupt Configuration:**
    * Configure pin `PD11` as `GPIO_EXTI11`.
    * Enable **System Core -> NVIC -> `EXTI line[15:10] interrupts`**.

<img width="1516" height="571" alt="5" src="https://github.com/user-attachments/assets/023c0720-77fb-456c-8398-d7f0948f367a" />


5.  **Generate Code:** Save the `.ioc` file (Ctrl+S).

### 6. Code Setup & Deployment (Drop-in Ready) 🚀

This project uses a modular structure. After generating the base project from CubeIDE:

1.  **Required Files:** You need the following three files from this repository:
    * `LSM6DSL.h` (Sensor driver header) -> Place in **`Core/Inc/`**
    * `main.c` (Main application logic) -> **Replace** the existing file in **`Core/Src/`**
2.  **Build & Flash:**
    * Clean and Build the project in STM32CubeIDE.
    * Flash the firmware (`Run As` > `STM32 Application`).

### 7. Running & Verification ✅

1.  **Open Serial Terminal:** Connect using the COM port for the STLINK Virtual COM Port.
2.  **Configure Terminal:** Use **115200 Baud, 8N1**.
3.  **Reset Board:** Press the **Reset button (B2 - Black)**.
4.  **Observe Output:** The terminal should display continuous accelerometer readings. Tilt the board to verify the values change.
    ```
    LSM6DSL Accel X:  [X_VALUE] mg
    LSM6DSL Accel Y:  [Y_VALUE] mg
    LSM6DSL Accel Z:  [Z_VALUE] mg
    --------------------
    ```
  
---

## 🔗 Connect with the Embedded Engineer

If you find this project useful or have questions about embedded systems development, feel free to connect!

* [**LinkedIn Profile**](https://www.linkedin.com/in/laingam98)

---
