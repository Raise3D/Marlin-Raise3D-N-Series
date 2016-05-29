V1.1.1 Update
1. Reverted PID value back to v1.0 version.


V1.1 Update
1. Fixed flowrate command M221 problem. Previous official version won't take effect under certain situations.
2. Changed PID value for V2 hotend.

#Tips: Please download the latest arduino addons for Marlin from the official Marlin repository and install them in the library folder before compiling codes for Raise3D firmware.

# Marlin-Raise3D-N-Series
Modified Marlin firmware for Raise3D N Series Printers.

Compile the codes with Arduino IDE(versions above 1.0.5) or other compatible compliers. 
Take Arduino IDE as an example: 
1. Get the .hex file from the temporary build folder.(Select the 'Show verbose output during:  compilation' checkbox. After the compilation finished, you can see where the .hex file was stored.)
2. Rename the file extension to '.firm' file instead of '.hex' file.
3. Put it in a usb key or sdcard and insert it to the printer.
4. Select the '.firm' file from the 'Print Files' menu. The system will automatic apply new firmware to the motion controller.

Important Notes:
*Never change the serial port baudrate settings, this will cause the touchscreen cannot connect to the motion controller board. 
*Currently, native touchscreen application don't support to display serial port messages. Need to add a debug mode in future updates. Debugging still could be done via command lines.
*The motion controller board supports 'RepRapDiscount full graphic smart controller'. And it's plug and play(Rebooting needed). With the RepRapDiscount full graphic smart controller, you can adjust motion settings like accelerations and jerk on the fly. It would be very helpful to advanced users.
