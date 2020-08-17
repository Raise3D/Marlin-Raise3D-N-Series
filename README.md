# Marlin-Raise3D-N-Series  
Modified Marlin firmware for Raise3D N Series Printers.  

## Update History:  
#### v1.1.6-rev1:  
* Fixed a bug while heated bed was heating, the thermal_runaway function will operate invalid memory location to cause strange behaviour.  

## Update History:  
#### v1.1.6:  
* Add history tracking into thermal runaway function, code copied from latest marlin branch.  

#### v1.1.5:  
* Reimplemented thermal runaway function, added protection while changed by gcode.  
* Temperature reporting during heating period fixed.  


#### v1.1.4:  
* Enlarged thermal runaway protection range to fix the thermal error on certain machines(Thermal protection code contributed by Jetguy).  
* Add extruder number while throwing out max or min temperature error to help identify the corresponding thermalcouple.  


#### v1.1.3:  
* Reverted reset function to v1.1.1 implementation.  
* Add compile option for single extruder. (uncomment #define DUAL to get dual head version.) In case to avoid the damaged second thermocouple on single head machine to generate an error.  

#### v1.1.2:  
* Modified M112 kill function to implement fast stop feature.  

#### V1.1.1:  
* Reverted PID value back to v1.0 version.  

#### V1.1:  
* Fixed flowrate command M221 problem. Previous official version won't take effect under certain situations.  
* Changed PID value for V2 hotend.  

## Compilation guide:  
Compile the codes with Arduino IDE(version 1.0.5 suggested) or other compatible compliers.  
Take Arduino IDE as an example:  
* Please download the latest arduino addons for Marlin from the official Marlin repository and install them in the library folder before compiling codes for Raise3D firmware.  
* Make sure all the library folders under Arduino Addons directory are copied into arduino install directory before compilation. Or you will encounter an error that missing the u8glib.  
* Select **Arduino Mega2560 or Mega ADK** in menu tools->board.  
* Open 'Marlin.ino' and compile the whole sketch.  
* Click the verify button to compile the whole sketch.  
* Copy the **.hex** file from the temporary build folder.(Select the 'Show verbose output during:  compilation' checkbox. After the compilation finished, you can see where the .hex file was stored.)  
* Rename the file extension to **.firm** file instead of **.hex** file.  
* Put it in a usb key or sdcard and insert it to the printer.  
* Select the **.firm** file from the 'Print Files' menu. The system will automatic apply new firmware to the motion controller. 

### Important Notes:  
* Never change the serial port baudrate settings, this will cause the touchscreen cannot connect to the motion controller board.  
* Never change any serial communication protocle or it will make the touchscreen unresponding.  
* Currently, native touchscreen application don't support to display serial port messages. Need to add a debug mode in future updates. Debugging still could be done via command lines.  
* The motion controller board supports 'RepRapDiscount full graphic smart controller'. And it's plug and play(Rebooting needed). With the RepRapDiscount full graphic smart controller, you can adjust motion settings like accelerations and jerk on the fly. It would be very helpful to advanced users.  

## High temperature extrusion mod compilation guide:  
* Compile the original version.  
* Change the **HEATER_0_MAXTEMP** & **HEATER_1_MAXTEMP** to 400. 400C is safe for 380C printing. You need to make this limit higher in order to give some space for PID tuning. The max allowed temperature for hotend is 380C.  
```  
Configuration.h  
#define HEATER_0_MAXTEMP 320 (Change it to 400)  
#define HEATER_1_MAXTEMP 320 (Change it to 400)
```  
* Compile the firmware and flash it into the motion controller board.  
* Add physical insulation outside the heating block. Be careful that the insulation don't cover the coldend and thermal break.  
* Unplug the motion controller board from the touchscreen and attach it to a PC. Use software like printrun to send gcode **M303 S350** to activate autotune function. Once it finished, copy the new Kp Ki and Kd and replace the old ones in the firmware.  
```  
Configuration.h 
#define  DEFAULT_Kp 14.49 (Replace with new value)  
#define  DEFAULT_Ki 0.8 (Replace with new value)  
#define  DEFAULT_Kd 65.52 (Replace with new value)  
```  
* Recompile the firmware and flash it in the motion controller board. (Or use gcode **M301 P19.56 I0.71 D134.26** in the start gcode to change the PID parameter.)  
* Reconnect the motion controller board back to the touchscreen and start to print.  
* The touchscreen software has a software limit on temperature operating. So a 'RepRapDiscount full graphic smart controller' is highly recommanded for temperature and parameters debugging. And touchscreen could still be your front interface to print files. We don't have temperature limit while executing from gcode.  
