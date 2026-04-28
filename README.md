# Hoverboard Robot Control System

This repository provides a complete guide to repurpose a **hoverboard controller** (with GD32F103 or STM32F103 chip) into a powerful robot driver. It uses the open-source [`EFeru/hoverboard-firmware-hack-FOC`](https://github.com/EFeru/hoverboard-firmware-hack-FOC) firmware.

## 🤔 What is a "Hoverboard" for Robotics?

- **What it has:** Two powerful brushless motors, a motor controller board (the "brain"), a 36V battery, and two sensor cables.
- **What it lacks:** Hall sensors (for super-precise motor position) are not used. The firmware uses **Field Oriented Control (FOC)** based on motor current sensing.
- **The challenge:** The original firmware is locked to balance gyroscopes. To control it for a robot, you **must flash custom firmware**.

                    ![image_alt](https://github.com/hassanjizzine0-afk/hoverboard-control-/blob/5181ca5e1dca4890f59d992844e98c160d92d2f2/mainboard_pinout.png)![image_alt](https://github.com/hassanjizzine0-afk/hoverboard-control-/blob/a6b83ae5cd32082fe9cf6ede1069fcf2c654b9a7/photo0089703_M2.jpg)











## 🎯 Your Two Control Methods

This repo shows you how to configure and flash that same base firmware for two different control styles. **You will choose and flash ONE variant at a time.**

| Control Method | Goal | Firmware Variant | Key Hardware |
| :--- | :--- | :--- | :--- |
| **RC Control** (Folder: `rc-control/`) | Drive with a standard RC transmitter (e.g., RadioMaster TX12) | `VARIANT_PPM` or `VARIANT_PWM` | RC Receiver |
| **UART/ROS Control** (Folder: `uart-ros-control/`) | Send velocity commands from a Raspberry Pi (ROS2 Humble) | `VARIANT_USART` | USB-to-TTL Adapter |

## 🛠️ Prerequisites (The Same for Both Methods)

1.  **Hardware:**
    *   Hoverboard with its 36V battery.
    *   **ST-Link V2 programmer** (required to flash the firmware).
    *   **Multimeter** (to safely verify wires!).
  
![image_alt](https://github.com/hassanjizzine0-afk/hoverboard-control-/blob/20e7e078dae673a9ef120dd9b184c103beff5304/photo0089704_M2.jpg)




      
2.  **Software (on your Ubuntu PC):**
    *   **Visual Studio Code** with the **PlatformIO IDE extension** installed.
    *   *(PlatformIO automatically installs the ARM GCC compiler and tools needed to build the firmware).*

## ⚠️ CRITICAL SAFETY WARNINGS

**Read this before connecting any wires!**

- **The red wire in the hoverboard's sensor cables carries 15V** – it will destroy any 5V device (RC receiver, Raspberry Pi, Arduino).
- **The black wire may NOT be ground** – some boards put 15V on black! **ALWAYS verify with a multimeter** between a suspected ground wire and the battery negative (-) terminal. Only a **0V** reading is true Ground.
- **Use the RIGHT sensor cable (shorter one, USART3)** – it is 5V tolerant and less noisy.

## 🚀 How to Use This Repository

1.  **Clone this repo** or download it as a ZIP.
2.  **Download the original source code** from [`EFeru/hoverboard-firmware-hack-FOC`](https://github.com/EFeru/hoverboard-firmware-hack-FOC) (as a ZIP) and place its contents into the `common/firmware-source/` folder.
3.  **Open the `common/firmware-source` folder in VS Code.** PlatformIO will detect the project.
4.  **Decide your control method:**
    *   For **RC control**, copy the `platformio.ini` from `rc-control/` into the firmware root.
    *   For **UART/ROS control**, copy the `platformio.ini` from `uart-ros-control/` into the firmware root.
5.  **Edit the `config.h` file** inside the firmware as needed (the folder-specific READMEs explain this).
6.  **Connect your ST-Link** to the hoverboard's SWD header (GND, SWDIO, SWCLK) and power the board with the battery.
7.  **In VS Code, click the PlatformIO toolbar icon (ant head) → Upload (→).** This will build and flash the firmware.
8.  **Follow the wiring and calibration guides** in the method-specific folder (`rc-control/` or `uart-ros-control/`).

## 📁 Folder Guide

*   **`rc-control/`**: Step-by-step for PPM/PWM wiring, transmitter setup (EdgeTX), and calibration.
*   **`uart-ros-control/`**: Guide for hardware wiring (USB-to-TTL), ROS2 driver installation, and publishing `/cmd_vel`.
*   **`common/`**: Pinout diagrams, ST-Link flashing details, power safety checklists, and troubleshooting.
*   **`docs/`**: Extended safety warnings.

## 🔗 Original Source

This entire project is based on the excellent work by **EFeru**:
[https://github.com/EFeru/hoverboard-firmware-hack-FOC.git](https://github.com/EFeru/hoverboard-firmware-hack-FOC.git)

All credit for the motor control firmware goes to that project. This repository is a **configuration guide and usage example** for two specific robot control scenarios.# hoverboard-control-
