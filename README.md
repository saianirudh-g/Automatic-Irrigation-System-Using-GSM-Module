# Automatic Irrigation System Using GSM Module

A micro-controller-based automated irrigation project designed to conserve water, reduce manpower, and provide real-time soil moisture sensing and control via cellular network communications[cite: 1].

---

## 📌 Project Overview

This project implements an automated, real-time soil monitoring and irrigation control system[cite: 1]. By interfacing soil moisture sensors with a central microcontroller and a GSM module, the system automatically regulates water supply to fields via a water pump and solenoid, while sending notifications/updates directly to a user's mobile device[cite: 1].

### Objectives
* **Conserve Water:** Deliver precise amounts of water based on continuous soil moisture readings[cite: 1].
* **Reduce Manpower:** Automate manual agricultural tasks and field monitoring[cite: 1].
* **Real-time Monitoring & Control:** Provide instant telemetry and remote management via GSM using standard AT commands[cite: 1].

---

## 👥 Team & Acknowledgments

* **Presented By (II B.Tech II Sem):** Sai Anirudh, Sai Srinivas, Satish, Vara Prasad, Ravi Chandra, Sudhamai, Hemanth, Swathi[cite: 1]
* **Guided By:** Professor Durga Prakash Sir (EEE Department, VIT)[cite: 1]

---

## 🏗️ System Architecture

[ Moisture Sensor ] ---> [ ADC ] <---> [ Master Controller ] <---> [ MAX232 ] <---> [ GSM Module ]
|                                         |
v                                         v
[ Solenoid / Relay Driver ]                   [ Android Mobile ]
|                                         |
v                                         v
[ Water Pump ]                              [ User ]

---

## 🛠️ Hardware Components & Resources

1. **Master Controller:** NXP LPC2129 (32-bit ARM7TDMI-S RISC Microcontroller)[cite: 1]
   * 256 KB Flash, 16 KB RAM, 4-channel 10-bit ADC, 2 UARTs, PWM outputs[cite: 1]
2. **GSM Module:** SIM900 GSM/GPRS Modem[cite: 1]
   * Dual-band (900/1800 MHz), TCP/IP protocol support, controlled via standard AT commands[cite: 1]
3. **Level Converter:** MAX232 (for RS232-to-TTL serial communication)[cite: 1]
4. **Soil Moisture Sensor:** Hydra Probe / Frequency Domain Moisture Sensor (Capacitance based)[cite: 1]
   * Measures soil moisture, temperature, dielectric permittivity, and conductivity[cite: 1]
5. **Actuator & Driver:** Relay Driver, Solenoid Valve, and Water Pump[cite: 1]
6. **Power Supply Unit**[cite: 1]

---

## 🔄 System Workflow & Operation

1. **Data Acquisition:** The soil moisture sensor continuously reads soil moisture levels and transmits analog voltage outputs to the microcontroller's ADC[cite: 1].
2. **Decision Making:** The LPC2129 microcontroller processes the analog inputs[cite: 1].
   * **If Moisture < Threshold:** The controller signals the relay driver to open the solenoid valve and activate the water pump[cite: 1].
   * **If Moisture >= Threshold:** The pump is deactivated to prevent overwatering[cite: 1].
3. **Communication:** The microcontroller communicates with the SIM900 GSM module via MAX232 using AT commands (e.g., `AT+CMGF=1`, `AT+CMGS="..."`) to alert the user's mobile device on irrigation status updates[cite: 1].

---

## 🚀 Getting Started

### Prerequisites
* Keil uVision IDE (for LPC2129 ARM C programming)[cite: 1]
* Flash Magic or Keil ISP Utility (for flashing firmware)
* Hardware setup matching the system architecture diagram[cite: 1]

### Installation & Deployment
1. Connect the GSM Module to UART0 via the MAX232 level converter[cite: 1].
2. Connect the soil moisture sensor analog output pin to the ADC input of the LPC2129[cite: 1].
3. Connect the output GPIO pin to the relay driver circuit controlling the water pump/solenoid[cite: 1].
4. Insert an active 2G SIM card into the SIM900 module[cite: 1].
5. Compile and flash the project firmware onto the LPC2129 microcontroller using Keil[cite: 1].

---

## 🎯 Conclusion

This system presents an efficient, automated solution for modern precision agriculture[cite: 1]. By replacing manual intervention with automated sensor feedback and GSM alert systems, farmers can conserve water resources and maximize yield with minimal effort[cite: 1].
