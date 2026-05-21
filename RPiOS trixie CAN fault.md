## RPiOS "Trixie" issue with CAN and CAN_RAW drivers ##
A  RPi4b running Bookworm with a Waveshare RS485/CAN HAT installed will not communicate on the CAN-bus with an identical RPi4b running Trixie.  
In order to simplify the conditions for reproducing the fault, the simple "cansend" and "candump" comand-line programs from "can-utils" have been used, and show the communications working between 2 Bookworm systems, and failing with the Bookworm-to-Trixe setup.  

### RPi4b set-up ###  
Install the Waveshare RS485/CAN HAT, and edit the edit the config.txt file in the boot partition:

  ``sudo nano /boot/config.txt  (or possibly /boot/firmware/config.txt)``  

Add this line to the file:

  ``dtoverlay=mcp2515-can0,oscillator=12000000,interrupt=25,spimaxfrequency=2000000``   
  
  This assumes the manufacturer installed a 12 MHz crystal oscillator on ythe RS485/CAN hat.
  
  Enable SPI communication with the help of the raspi-config tool. Open it by running command:

  ``sudo raspi-config``  

Go to section Interface Options → SPI and select Yes to enable the SPI interface, and reboot.    
run  
```
    sudo modprobe can
    sudo modprobe can_raw
````
To verify that the SocketCAN related kernel modules loaded properly, run:
