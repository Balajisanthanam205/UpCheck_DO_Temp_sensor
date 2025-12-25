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
	• D4 pin – Data cable (yellow colour).   
	• 3.3V pin – power cable (Red colour).   
	• GND pin – ground cable (Black colour).   
This Temperature sensor will only work with the help of pull up resistor (4.7K) in between 3.3V and D4 pins as shown in the picture.

![Temp sensor circute](https://github.com/user-attachments/assets/366887ef-cf3a-4381-a87c-2738fa362c51)  **Fig No.03: Temperature Sensor Circute with (4.7K) resistor in ESP32.**

This is to measure the Water temperature.
	
**[Temperature Sensor Code (for Esp32)](https://github.com/Balajisanthanam205/UpCheck_DO_Temp_sensor/blob/main/Temp%20Sensor%20Code%20(Esp32))**	

**Sample output:**	

	Temperature: 40.00 °C	
	Temperature: 40.00 °C	
	Temperature: 39.94 °C	
	Temperature: 39.94 °C	
	Temperature: 39.94 °C	
	Temperature: 39.94 °C	
	Temperature: 39.94 °C	

**Step 3:** Making the probe ready for the Calibration/DO reading.

**Thing needed:**   
	• NaOH solution (0.5 mol).   
	• Distilled water.   
		
First make the NaOH solution of 0.5 mol to achieve that take 100 ml of distilled water and add 2 grams of NaOH crystal/Pilets and dissolve it properly,
this will generate some Heat wait for few minutes to get rid of that heat.


Next remove the head of the Probe in the DO sensor with care don’t damage the membrane at the tip it is very sensitive,
And fill the NaOH solution in that head and screw It back in the prob and clean the outside with the distilled water to get rid of the over flowed NaOH solution and make it dry with tissue paper (don’t touch the tip of the prob).


<img width="1057" height="640" alt="prob prepration" src="https://github.com/user-attachments/assets/c45fb067-e7a3-4e59-9b29-5e93f8f1c7d0" /> Fig No.04:Probe Prepration.

Make sure there is no bubble or air pockets in that solution when you close that head.

**Step 4:** Setup the DO sensor with the Microcontroller (Arduino UNO) for initial calibration.	

**Pin configuration:**   
	• A1 pin – Data cable (Blue colour).   
	• 5V pin – power cable (Red colour).   
	• GND pin – ground cable (Black colour). 


This DO sensor need min of 5V for proper working and 5.5V in the max limit (handle 3.3 V to 5.5 V) refer the pictures for move understanding.

![Arduno UNO set up for DO sensor](https://github.com/user-attachments/assets/ec41b42f-2d30-48c6-93a8-44a4e3d0bc72) **Fig No.05: Arduino UNO setup.** 
![DO sensor convertor board](https://github.com/user-attachments/assets/72c84e36-f572-4538-9c2f-2fb9a36a9c60) **Fig No.06:DO Sensor Data Convertor board.** 
![Full DO sensor setup](https://github.com/user-attachments/assets/de28ec89-ef3f-4c62-9e93-9574af4b2fc4) **Fig No.07:DO Sensor Full Setup.**


[Code for Calibration](https://github.com/Balajisanthanam205/UpCheck_DO_Temp_sensor/blob/main/Calibration%20Code%20for%20DO%20sensor%20(UNO))
Place the Prob in the distilled water and start to take the reading for calibration.

**Sample Output:**	

	raw:	212	Voltage(mv)1035	
	raw:	211	Voltage(mv)1030
	raw:	212	Voltage(mv)1035
	raw:	213	Voltage(mv)1040
	raw:	291	Voltage(mv)1420
	raw:	327	Voltage(mv)1596
	raw:	341	Voltage(mv)1665

**Issues may face and solutions for that Issues:**

1)	We may get Output as:


		raw:	0	Voltage(mv)0
		raw:	0	Voltage(mv)0
		raw:	0	Voltage(mv)0
		raw:	0	Voltage(mv)0
		raw:	0	Voltage(mv)0
		raw:	0	Voltage(mv)0
		raw:	0	Voltage(mv)0
	**Solution:** make sure you Give the Input Voltage of 5V for the DO sensor to avoid this issue.

This is just to check that the sensor is working there is no major issue in that sensor like damage in the electrode and all, in the next step only the actual calibration starts.

**Step 5:** Calibration of DO sensor.

**There is Two types of calibration first:**   
		• Single point calibration (works only of one singe temperature Eg. 25.C).   
		• Two point calibration (works for any temperature Eg. 15.C, 20.C, 25.C and more).   

**Thing need for Two-point Calibration:**   
		• One cup with hot distilled water not more that 40.C.   
		• One cup with cold distilled water aprox of 15.C or (less than the hot value).
		
First go with either hot or cold water dip the DO sensor prob in that cup of water and start to read the Voltage reading in the serial monitor, give an gentil move movement to avoid the air bubble in prob head and wait until the voltage to be stable and note the value **(Voltage and corresponding Temperature of the water)**.


**High Temprature**
**Sample output of Temperature sensor:**	

	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
	Temperature: 34.44 °C
**sample output for High Temp (DO sensor):**	

	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751
	raw:	154	Voltage(mv)751

**Sample output of Temperature sensor:**	

	Temperature: 14.31 °C
	Temperature: 14.25 °C
	Temperature: 14.19 °C
	Temperature: 14.19 °C
	Temperature: 14.13 °C
	Temperature: 14.13 °C
	Temperature: 14.06 °C
	Temperature: 14.06 °C
**sample output for Low Temp:**		

	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463
	raw:	95	Voltage(mv)463


**As a result of Two-point calibration we got 4-Values**   
	• HIGH TEMP - 34.   
	• VOLTAGE VALUE - 751 (mV).   
	• LOW TEMP - 14. 
	• VOLTAGE VALUE - 463 (mV).   







