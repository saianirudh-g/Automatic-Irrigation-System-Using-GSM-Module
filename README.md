# Automatic Irrigation System Using GSM Module

## Overview

The **Automatic Irrigation System Using GSM Module** is designed to automate the irrigation process by continuously monitoring soil moisture conditions and controlling a water pump based on the measured moisture level.

The system uses a **soil moisture sensor**, **microcontroller**, **relay driver**, **water pump**, **MAX232 interface**, and **GSM module** to provide automatic irrigation and remote notification to the user.

The main objective of this project is to reduce manual effort, conserve water, and provide real-time monitoring and control of irrigation.

---

## Objectives

- Reduce manpower required for irrigation.
- Conserve water by supplying water only when required.
- Monitor soil moisture in real time.
- Automatically control the irrigation water pump.
- Interface the soil moisture sensor with the microcontroller.
- Communicate irrigation information to the user through GSM.
- Notify the user when irrigation starts and stops.

---

## System Architecture

The basic architecture of the system is:

```text
                           +--------------------+
                           |       USER         |
                           +---------^----------+
                                     |
                              Android Mobile
                                     ^
                                     |
                              +------+------+
                              |     GSM     |
                              +------+------+
                                     |
                                 MAX232
                                     |
                                     v
+----------------+    +-----+   +----------------------+
| Soil Moisture  |--->| ADC |-->| Master Controller    |
| Sensor         |    +-----+   |      32-bit          |
+----------------+              +----------+-----------+
                                           |
                                           v
                                      +---------+
                                      |Solenoid |
                                      +----+----+
                                           |
                                           v
                                    +-------------+
                                    | Relay Driver|
                                    +------+------+
                                           |
                                           v
                                    +-------------+
                                    | Water Pump  |
                                    +-------------+
```

---

## Major Components

The project mainly consists of:

| Component | Purpose |
|-----------|---------|
| Soil Moisture Sensor | Measures the moisture present in soil |
| ADC | Converts the sensor signal into a form usable by the controller |
| LPC2129 Microcontroller | Processes moisture data and controls irrigation |
| Relay Driver | Drives the relay/pump control circuit |
| Solenoid | Controls water flow |
| Water Pump | Supplies water to the plants |
| MAX232 | Provides communication-level conversion |
| GSM Module | Sends information to the user's mobile phone |
| Android Mobile | Receives irrigation information |
| Power Supply | Provides the required operating power |

---

## Soil Moisture Sensor

The soil moisture sensor acts as the **feedback element** of the irrigation system.

The sensor measures the moisture condition of the soil and provides the information to the microcontroller.

Soil moisture measurement methods can be broadly classified as:

```text
                  SOIL MOISTURE MEASUREMENTS
                           |
              +------------+------------+
              |                         |
        DIRECT METHODS              INDIRECT METHODS
              |                         |
      Thermo-Gravimetric              Volumetric
      Thermo-Volumetric               Tensiometric
```

The project discusses frequency-domain moisture sensing using a capacitance-based sensor.

---

## Soil Moisture Sensor Types

```text
                   SOIL MOISTURE SENSORS
                           |
              +------------+-------------+
              |                          |
          VOLUMETRIC                 TENSIOMETRIC
              |                          |
       +------+------+                Gypsum Block
       |      |      |
      TDR    FDR   Neutron
            Sensor   Probe
```

### FDR

**Frequency Domain Reflectometry (FDR)** is one of the methods used for measuring soil moisture.

A capacitance-based sensor can be used to determine changes in the dielectric properties of the soil caused by changes in moisture.

---

## Hydra Probe

The presentation discusses the **Hydra Probe** as an example of a soil moisture sensing device.

### Characteristics

- Relatively inexpensive and widely used.
- Measures the real and imaginary components of the soil dielectric constant.
- Operates at approximately **50 MHz**.
- Installed directly in the soil for in-situ measurement.
- Can be installed at different depths.
- Typical power supply range: **7–30 V DC**.

### Hydra Probe Measurements

The probe can measure:

- Soil moisture
- Temperature
- Electrical conductivity
- Dielectric permittivity

### Probe Construction

The Hydra Probe consists of:

- A cylindrical sensor head.
- Four sensing tines.
- Approximately 0.3 cm diameter tines.
- Tines extending approximately 5.8 cm.
- Temperature sensing capability.

The tines act as waveguides and are inserted into the soil.

The probe converts the measured signal response into dielectric permittivity, which can be related to soil moisture.

### Hydra Probe Versions

The Hydra Probe is available in:

- SDI-12
- RS-485
- Analog

For the analog version:

- Fast measurement rate.
- Output consists of four voltage signals.

---

## Microcontroller

The system uses the **NXP LPC2129** 32-bit microcontroller.

The LPC2129 is based on the **ARM7TDMI-S** architecture.

### LPC2129 Features

- 32-bit RISC microcontroller
- 256 KB on-chip Flash ROM
- In-System Programming (ISP)
- In-Application Programming (IAP)
- 16 KB RAM
- 9 external interrupts
- Two UART interfaces
- I2C serial interface
- Two SPI serial interfaces
- Two timers
- PWM unit with up to six PWM outputs
- 4-channel 10-bit ADC
- Two CAN channels
- Real-Time Clock
- Watchdog Timer
- 46 general-purpose I/O pins
- CPU clock up to 60 MHz
- On-chip oscillator
- On-chip PLL

---

## GSM Module

**GSM** stands for:

> Global System for Mobile Communications

The GSM module is used to communicate between the irrigation controller and the user's mobile phone.

The GSM technology described in this project operates using second-generation cellular communication.

### GSM Features

- Dual-band GSM/GPRS operation
- 900/1800 MHz operation
- Configurable baud rate
- SIM card holder
- Network status LED
- Built-in TCP/IP protocol support

---

## GSM Working Principle

A GSM modem communicates with the microcontroller using a serial communication interface.

GSM modems are controlled using **AT Commands**.

### AT Commands

`AT` stands for:

```text
Attention
```

Commands sent to the GSM modem begin with:

```text
AT
```

The GSM/GPRS module consists of:

- GSM/GPRS modem
- Power supply circuitry
- Communication interfaces
- SIM card interface
- Antenna interface
- Network status indication

---

## GSM Module Hardware

A typical GSM module used in the project contains:

- GSM module
- SIM card holder
- Antenna
- DB9 serial connector
- GSM ON switch
- Power LED
- Network LED
- GSM enable status LED
- DC input socket
- Voltage regulator
- Bridge rectifier
- On/Off switch

---

## GSM Modem Interfacing With Microcontroller

The GSM modem is connected to the microcontroller through a serial communication interface.

```text
+----------------+
| Microcontroller|
|     UART       |
+-------+--------+
        |
        | TTL Level
        |
        v
+----------------+
|     MAX232     |
+-------+--------+
        |
        | RS232 Level
        |
        v
+----------------+
|   GSM Modem    |
+----------------+
        |
        v
   Mobile User
```

### MAX232

The **MAX232** is used because the voltage levels used by the microcontroller and RS232 communication interface are different.

Its main purpose is:

```text
TTL Logic Level
       |
       v
    MAX232
       |
       v
RS232 Logic Level
```

The MAX232 therefore provides the required communication interface between the microcontroller and GSM modem.

---

## Irrigation Control Logic

The system continuously checks the soil moisture level.

The project uses a moisture threshold of approximately:

```text
50%
```

The basic decision logic is:

```text
IF Soil Moisture < 50%
    Start Irrigation
    Turn ON Water Pump
    Inform User
ELSE
    Continue Monitoring
END IF
```

When sufficient soil moisture is reached:

```text
Stop Irrigation
Turn OFF Water Pump
Inform User
```

---

## System Flowchart

```text
                    +---------+
                    |  START  |
                    +----+----+
                         |
                         v
               +-------------------+
               | Check Soil        |
               | Moisture Level    |
               +---------+---------+
                         |
                         v
                    +---------+
                    | M < 50%?|
                    +----+----+
                       /   \
                    YES     NO
                     |       |
                     |       v
                     |   Continue /
                     |   Stop
                     |
                     v
             +-------------------+
             | Start Irrigation  |
             +---------+---------+
                       |
                       v
             +-------------------+
             | Initialize Pump   |
             | and Water System  |
             +---------+---------+
                       |
                       v
             +-------------------+
             | Send Report to    |
             | User Through GSM  |
             +---------+---------+
                       |
                       v
             +-------------------+
             | Monitor Moisture  |
             +---------+---------+
                       |
                       v
             +-------------------+
             | Stop Pump When    |
             | Threshold Reached |
             +---------+---------+
                       |
                       v
             +-------------------+
             | Notify User       |
             +---------+---------+
                       |
                       v
                    +------+
                    | STOP |
                    +------+
```

---

## Project Execution Steps

### Step 1 — Measure Soil Moisture

The soil moisture sensor continuously measures the amount of moisture present in the soil.

```text
Soil
  |
  v
Moisture Sensor
  |
  v
Microcontroller
```

---

### Step 2 — Compare With Threshold

The sensor reading is sent to the microcontroller.

The microcontroller compares the measured value with the predefined threshold.

```text
Sensor Reading
      |
      v
Microcontroller
      |
      v
Compare with 50% Threshold
```

---

### Step 3 — Start Irrigation

If the sensor input value is below approximately **50%**, the soil requires additional water.

The controller then:

1. Activates the irrigation system.
2. Starts the water pump.
3. Supplies water to the plants.
4. Sends information to the user through the GSM system.

```text
Moisture < 50%
      |
      v
Start Pump
      |
      v
Irrigation Starts
      |
      v
Notify User
```

---

### Step 4 — Continue Monitoring

While the pump is operating, the system continues measuring soil moisture.

```text
Pump ON
   |
   v
Water Plants
   |
   v
Read Moisture
   |
   v
Compare Threshold
```

---

### Step 5 — Stop Irrigation

Once the soil moisture reaches the required threshold, the microcontroller stops the water pump.

```text
Required Moisture Reached
          |
          v
      Pump OFF
```

---

### Step 6 — Notify User

After the pump stops, the user is again informed through mobile communication.

```text
Pump OFF
    |
    v
GSM Module
    |
    v
Mobile Notification
```

---

## Complete Working Sequence

```text
Soil Moisture
     |
     v
Moisture Sensor
     |
     v
ADC
     |
     v
LPC2129 Microcontroller
     |
     +---------------------------+
     |                           |
     v                           v
Relay Driver                  MAX232
     |                           |
     v                           v
Solenoid                     GSM Module
     |                           |
     v                           v
Water Pump                 Android Mobile
     |                           |
     v                           v
Irrigation                      User
```

---

## Working

The complete operation can be summarized as follows:

1. The moisture sensor measures the moisture present in the soil.
2. The sensor output is provided to the microcontroller.
3. The microcontroller compares the measured moisture value against a predefined threshold.
4. If the soil moisture value is below approximately 50%, irrigation is required.
5. The controller activates the relay driver.
6. The relay/solenoid control system starts the water pump.
7. Water is supplied to the plants.
8. The GSM module informs the user about the irrigation status.
9. The controller continues reading the soil moisture value.
10. When the required moisture level is reached, the controller switches the pump OFF.
11. The user is again notified through the GSM/mobile communication system.

---

## Advantages

The project is intended to provide:

- Automatic irrigation control.
- Reduced manual intervention.
- Water conservation.
- Real-time soil moisture monitoring.
- Remote irrigation status information.
- Better utilization of available water.
- Automatic pump control based on soil condition.

---

## Applications

The system concept can be used for:

- Agricultural irrigation
- Gardens
- Plant nurseries
- Greenhouses
- Farm irrigation monitoring
- Soil moisture monitoring systems

---

## Conclusion

The **Automatic Irrigation System Using GSM Module** provides an automated method for monitoring soil moisture and controlling irrigation.

By continuously checking soil moisture conditions, the system can operate the water pump when irrigation is required and stop watering after the desired moisture level is achieved.

GSM communication allows the irrigation status to be communicated to the user through a mobile device.

The project demonstrates a reliable and efficient approach for monitoring environmental parameters and observing changes in soil conditions.

---

## Project Team

### Presented By

- Sai Anirudh
- Sai Srinivas
- Satish
- Vara Prasad
- Ravi Chandra
- Sudhamai
- Hemanth
- Swathi

### Guided By

**Prof. Durga Prakash**

### Department

**Electrical and Electronics Engineering (EEE)**

**Vishnu Institute of Technology**

---

## References

The presentation refers to the following resources:

1. Engineers Garage — GSM/GPRS Modules
   - `www.engineersgarage.com/articles/gsm-gprs-modules`

2. EdgeFX — GSM Interfacing with 8051 Microcontroller
   - `www.edgefx.in/gsm-interfacing-8051-microcontroller/`

3. Stevens Water — Hydra Probe
   - `www.stevenswater.com/catalog/Stevens-Hydra-Probe.aspx`

4. IJERT — Smart Irrigation System Using Wireless Sensor Network

5. NXP / Keil — LPC2129 Microcontroller Documentation

---

## Repository Structure

```text
Automatic-Irrigation-System-Using-GSM-Module/
│
├── README.md
├── docs/
│   ├── project-presentation.pptx
│   ├── architecture.png
│   └── flowchart.png
│
├── hardware/
│   ├── circuit-diagram.png
│   └── gsm-interface.png
│
└── images/
    ├── moisture-sensor.png
    ├── hydra-probe.png
    ├── gsm-module.png
    └── irrigation-system.png
```

> **Note:** The original project presentation describes the system architecture,
> hardware, GSM interface, flowchart, and execution procedure. Firmware/source
> code is not included in the supplied presentation.

---

## Future Improvements

Possible extensions of the project can include:

- Multiple soil moisture sensing locations
- Improved irrigation scheduling
- Data logging
- Remote monitoring dashboard
- Additional environmental sensors
- Automatic fault indication

---

## License

This repository is intended for **educational and academic project purposes**.

---

## Acknowledgment

We sincerely thank our project guide, faculty members, and department for their
support and guidance during the development of the project.

---

# Thank You
