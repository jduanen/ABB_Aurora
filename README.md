# ABB_Aurora
Web-based monitor for ABB Aurora solar panel inverters

Derived from ABB Power One Aurora: Web Interface Module (WIM), see: 
  * https://www.instructables.com/Inverter-Aurora-ABB-Power-One-Web-Monitor-WIM-With/
  * https://www.pcbway.com/project/shareproject/ABB__Power_One__Aurora_Web_Solar_Inverter_Monitor__WIM___server_PCB.html?from=mischianti723

* TODO
  - Model and print Case
  - 

## Software

* how to install
  - build from ino file on github
    * ????
  - upload pre-built bin file from github
    * ????

## Protocol

* link
  - 19200 baud, 1 stop bit, no parity
* command message
  - fixed length: 8B + 2B (checksum)
    * 0: address
      - value between 2 and 63
      - normally is set to '2'
      - defined in inverter's menu
    * 1: command
    * [2-7]: data bytes (B2-B7)
    * 8: CRC_L
    * 9: CRC_H
* response message
  - fixed length: 6B + 2B (checksum)
    * 0: transmission state
      - 0: ok
      - 51: unimplemented Command
      - 52: variable doesn't exist
      - 53: variable value out of range
      - 54: EEprom not accessible
      - 55: Service Mode not toggled
      - 56: cannot send Command to internal controller
      - 57: Command not executed
      - 58: variable is not available, retry
    * 1: global state (state of the addressed device)
      - ?
    * [2-5]: data bytes (B2-B5)
    * 6: CRC_L
    * 7: CRC_H

## Hardware

* Specs/Pinouts
  - WeMos D1 mini ESP8266
    * CH340 USB interface
    * uUSB connector
    * 11 GPIO, interrupt/PWM/I2C/one-wire (not D0)
    * 1 ADC input (<= 3.2V)
    * 1MB FLASH
  - WeMos D1 mini LiPo Battery Shield
    * Charging Voltage: 10V max, 5V typ
    * Charging Current: 1A max
    * LiPo Battery Voltage: 3.3-4.2V
    * Boost Power Supply: 5V @ 1A max
    * Ports
      - LiPo Battery: PH2-2.0mm (3.3-4.2V)
      - Charging Port: micro USB (5V)
      - Green LED: charging complete
      - Red LED: charging
      - J1: max charging current (0.5A or 1.0A)
      - J2: connect battery to ESP8266 pin A0

* BOM:
Amount  Part Type               Properties
------  ----------------------  ---------------------------------------------
  1     WeMos D1 Battery        Shield
  1     WeMos D1 Mini           CPU: ESP-8266EX
  1     MAX485                  Package: DIL08
  1     LD1117V33               Voltage: 3.3V; package 78xxl; chip LD1117VXX
  2     Electrolytic Capacitor  Capacitance: 10µF
  1     104Ω Resistor           Pin Spacing: 400 mil; tolerance: ±5%;
==> replace the 104Ω with 120Ω
  2     150Ω Resistor           Pin Spacing: 400 mil; tolerance: ±5%;
  1     Camdenboss CTB0158-2    Pin Spacing: 0.2in (5.08mm); hole size: 2.7mm
  1     Male header – 1 pins    Pin Spacing: 0.1in (2.54mm)
  6     Male header – 2 pins    Pin Spacing: 0.1in (2.54mm)
  1     Male header – 6 pins    Pin Spacing: 0.1in (2.54mm)
  1     18650                   LiPo Battery

## Links
  - https://www.instructables.com/Inverter-Aurora-ABB-Power-One-Web-Monitor-WIM-With/
  - https://www.pcbway.com/project/shareproject/ABB__Power_One__Aurora_Web_Solar_Inverter_Monitor__WIM___server_PCB.html?from=mischianti723
  - https://www.wemos.cc/en/latest/d1_mini_shield/battery.html
  - https://github.com/xreef/Aurora_Web_Invert_Monitor/tree/master
  - https://mischianti.org/abb-aurora-pv-inverter-library-for-arduino-esp8266-and-esp32/
