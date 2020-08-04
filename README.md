# 3D Printer Filament Runout Sensor
This is a low filament detector base on the ATtiny13 - 8-bit AVR Microcontroller for your 3d printer. When your filament runs out it will sound the alarm and flash the RGB LED and with the proper firmware modifications and GCode, will pause your printer giving you time reload your filament.

[![Watch the demo video](https://mini-mods.com/wp-content/uploads/2020/01/video_shot.png)](https://www.youtube.com/embed/Nork3BS47Sg)

License
-------
<div align="center"><a rel="license" href="https://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Attribution-NonCommercial-ShareAlike" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /></div>

This project is licensed under the Attribution-NonCommercial-ShareAlike CC BY-NC-SA 4.0 license. The full legal text of the license may be found in the LICENSE.md file in this repository. For more information about this license, please visit 
the Creative Commons Foundation (https://creativecommons.org/licenses/by-nc-sa/4.0/).

Features
--------
* Low filament detector for your 3d printer.

* Detect filament diameter of 1.75mm, 2.85mm and 3.00mm.

* Can interface with a variety of 3D Printer Controller Board including:
	- RAMPS 1.2 and newer
	- RAMBo 1.2 and newer
	- Printrboard Rev B,C,D,E

* Supports Marlin 1.1.X or newer, RepRap and Octoprint 1.3.8 or higher.

* Can be daisy-chain using the extension port to handle many filaments simultaneously

* Audio and visual alerts.

* One button operation mode.

* Operational Voltage: 5V

* Compact PCB design (30.62mm x 25.90mm).

* Reverse polarity protection.

* Programming pins for future firmware upgrade.

* You can buy the latest version of this board fully assembled from [http://mini-mods.com](http://mini-mods.com)

----------
* Filament Runout Sensor Top.
![Filament Runout Sensor Top](pictures/top_white.png)

* Filament Runout Sensor Bottom.
![Filament Runout Sensor Bottom](pictures/bottom_white.png)
----------

Prerequisites
---------------------
1. Available Z+ endstop port on your 3D printer. 

2. Access to the source code for your existing printer.

3. Arduino IDE 1.8 or newer.

Software Configuration
----------------------
### Marlin Firmware

Modify Configuration.h on Filament Runout Sensors section uncomment the following line:

		#define FILAMENT_RUNOUT_SENSOR
			
In this case, I used the Z+ Port on a RAMPS Board (see other boards pinout on the Hardware Section), therefore you need to set <code>FIL_RUNOUT_PIN</code> in pins_RAMPS.h to 19, add the following line to the block of code:

		#define FIL_RUNOUT_PIN  19
			
Since the sensor has its own pull-up resisters comment the following line:

		//#define FIL_RUNOUT_PULLUP 
		
Also if you need to invert the logic of the sensor set to <code>true</code> the following line:

		#define FIL_RUNOUT_INVERTING false
		
Modify Configuration_adv.h in the section Advanced Pause, and uncomment the following line:

		#define ADVANCED_PAUSE_FEATURE
		
Once done, flash the modified firmware to your printer.

More information about the firmware configuration is available at the official Marlin Documentation [found here.](http://marlinfw.org/docs/configuration/configuration.html#filament-runout-sensor)


### OctoPrint Plugin

For Raspberry Pi with OctoPrint use this Plugin: [found here.](https://plugins.octoprint.org/plugins/filament_sensor_reloaded/)

Hardware Installation
---------------------
Once the firmware is configured and uploaded to your printer, Marlin will send M600 gcode to change the filament spool once the sensor is triggered.

The following images display the correct pin location for the installation for the Filament Runout Sensor.

* RAMPS 1.4 Pinout.
![ramps](pictures/ramps.png)

* RAMBo 1.2 Pinout.
![rambo](pictures/rambo.png)

* Printrboard Rev B,C,D,E Pinout.
![printrboard](pictures/printbrd.png)

If you have a Raspberry Pi with OctoPrint setup, use the plugin above in order to use this sensor, connected to the Raspberry Pi.

### Daisy-chain Configuration

This sensor can also be daisy-chain to handle as many extruders you have on your 3D printer and manage the filament spools independently if any of your filaments run out, Marlin will get notified as the sensor gets trigger and pause your printer without any additional configuration and using only the Z+ port on your board.

Basic Hardware Usage
--------------------
1.- When the filament is loaded the Green led will indicate normal operation.

2.- Once the sensor detects no filament, the alarm will start, along with a flashing Blue and Red led indicators.

3.- You can mute the alarm by pressing the push button, this will set the sensor in standby mode with an intermittent Blue led.

4.- After the filament is reloaded, the led indicator will switch back to Green.

Basic Maintenance
-----------------
This sensor contains a limit switch and dust or debris can cause false or changing readings. Clean dust by blowing on the sensor or disassembly to clean the limit switch.