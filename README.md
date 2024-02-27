# LED Controller

The LED Controller code will run on an Arduino Nano board, and controls a string of WS281x-type LEDs. Control commands are sent via the USB connector on the Arduino. The maximum number of LEDs supported is 300.

## Compiling and Uploading with the Arduino IDE

The code may uploaded (or flashed) onto the Arduino Nano board by loading it into the Arduino IDE program and using its 'Upload' function.  Arduino IDE version 1.8 or newer is required, and it can be downloaded from https://www.arduino.cc/en/Main/Software

The LEDCtrlr code will need to be downloaded and unpacked onto a computer. In the RotorHazard "LEDCtrlr" repository on GitHub, go to the releases page, click on the "Source code (zip)" link, download the file, and unpack the ".zip" file to a directory on your computer.

In the Arduino IDE, select "File | Open" and navigate to where the 'LEDCtrlr' directory is located, and click on the "LEDCtrlr.ino" file to open the project.  In the Arduino IDE the board type (under "Tools") will need to be set to match the Arduino -- the standard setup is:  for 'Board' select "Arduino Nano" and for 'Processor' select "ATMega328P" or "ATMega328P (Old Bootloader)", depending on the particular Arduino used.  If all is well, clicking on the 'Verify' button will successfully compile the code.

The Arduino module is plugged into the computer via its USB connector (and a USB cable). When connected, it will be assigned a serial-port name (like "COM3"). In the Arduino IDE the serial port (under "Tools | Port") will need to be set to match the connected Arduino.  (If you view the "Tools | Port" selections before and after connecting the Arduino, you should see its serial-port name appear.)  Clicking on the 'Upload' button should flash the code onto the Arduino processor. If the code has been successfully flashed, the LED on the Arduino board will flash once every four seconds.

The LED strip should be connected to the 'D3' pin (signal) and the 'GND' pin on the Arduino board. It is recommended to use a separate power source to power the LED strip.

## Connecting to the RotorHazard Server

Once the Arduino is flashed, it may be attached (via USB cable) to a USB port on the race timer (or computer that is running the RotorHazard server). RotorHazard server version 4.1.0 or later is required.

On the Raspberry Pi, an attached LEDCtrlr module will be referenced with a serial port name like "/dev/ttyUSB0". The command "ls /dev/ttyUSB*" will show the current USB serial ports. The "src/server/config.json" file for the RotorHazard server will need to be modified to have an entry like this in the "LED" section:
```
		"SERIAL_CTRLR_PORT": "/dev/ttyUSB0",
```

On a Windows computer, an attached LEDCtrlr module will be referenced with a serial port name like "COM3". The current ports may be viewed in the Windows Device Manager under "Ports (COM & LPT)" -- when the USB node is plugged in, its entry should appear.  It may be necessary to install or update its driver (named something like "USB-SERIAL"). The "src/server/config.json" file for the RotorHazard server will need to be modified to have an entry like this in the "LED" section:
```
		"SERIAL_CTRLR_PORT": "COM3",
```

The "LED_COUNT" entry in the "src/server/config.json" file should be updated to match the number of LEDs in the strip. If the LED colors appear incorrect, the "LED_STRIP" entry may be added or updated to match the strip, allowed values are:  'RGB', 'RBG', 'GRB', 'GBR', 'BRG', 'BGR' (default is 'GRB'). The other "LED_..." entries are not used with the LEDCtrlr.

If the LEDs are not operating properly, check the RotorHazard server log file for errors.
