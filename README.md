**ESP32 IoT Sensor Monitoring System using Supabase**

**Project Overview**
This project is an IoT-based real-time monitoring system that reads Temperature and Dissolved Oxygen (DO) values using an ESP32 microcontroller and transmits the data to Supabase.
A web-based dashboard built with HTML, CSS, and JavaScript retrieves and displays the sensor data in real time.

**The system is designed to demonstrate end-to-end IoT integration, covering:**
•	Sensor data acquisition
•	Cloud data storage
•	Web-based visualization

**Features**
1) Real-time sensor data acquisition using ESP32
2) Temperature monitoring (DS18B20-Digital)
3) Dissolved Oxygen (DO) sensor integration (Gravity Analog Dissolved Oxygen Sensor SKU SEN0237)
4) Cloud backend using Supabase
5) Web dashboard built with HTML, CSS, and JavaScript
6) Automatic data updates without page reload
7) Responsive UI (works on desktop and mobile)

**Tech Stack**

**Hardware**

1) Microcontroller (ESP32 Dev Modul)
2) Temperature Sensor (DS18B20)
    **Link:**
    https://www.elprocus.com/ds18b20-temperature-sensor/
3) Dissolved Oxygen (DO) Sensor (Gravity Analog Dissolved Oxygen Sensor SKU SEN0237)
     **Link:**
     https://wiki.dfrobot.com/Gravity__Analog_Dissolved_Oxygen_Sensor_SKU_SEN0237

**Software**

1) Frontend: HTML, CSS, JavaScript
2) Backend: Supabase (PostgreSQL + REST API)
3) Microcontroller Programming: Arduino IDE

**STEP-1**
We need an constant 5V supply for the DO sensor so we need to set the bug boost converter in this case we used

•	2-Lithiom iron battery.   
•	battery holder.   
•	converter.   
•	some jumpers.

First solder the converter with the battery holder in the input end and also solder the output end with two jumpers as shown in the picture. 

![bug boots (full setup)](https://github.com/user-attachments/assets/9f5a81b7-e408-43b5-828f-554007f8f425)    **Fig No.01: Full Setup.**      
![bug boots (close up for pin)](https://github.com/user-attachments/assets/22d2e131-9441-4328-aa49-5e60f8d2f778)    **Fig No.02: Pin Setup.**   

Adjust the POT Screw **(Potentiometer)** which will controller the Resistance with the help of Multi meter and screw drive for **(5V)**.
	
**Step 2:**
Setup the Temperature sensor (DS18B20) with Microcontroller (esp32).

**Pin configuration:**   
•	D4 pin – Data cable (yellow colour).   
•	3.3V pin – power cable (Red colour).   
•	GND pin – ground cable (Black colour).   
This Temperature sensor will only work with the help of pull up resistor (4.7K) in between 3.3V and D4 pins as shown in the picture.

![Temp sensor circute](https://github.com/user-attachments/assets/366887ef-cf3a-4381-a87c-2738fa362c51)  **Fig No.03: Temperature Sensor Circute with (4.7K) resistor in ESP32.**

This is to measure the Water temperature.

**Sample output:**
Temperature: 40.00 °C
Temperature: 40.00 °C
Temperature: 39.94 °C
Temperature: 39.94 °C
Temperature: 39.94 °C
Temperature: 39.94 °C
Temperature: 39.94 °C



