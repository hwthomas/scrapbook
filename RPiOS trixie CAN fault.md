## RPiOS "Trixie" issue with CAN and CAN_RAW drivers ##
A  RPi4b running Bookworm with Waveshare RS485/CAN HAT will not communicate with an identical RPi4b running Trixie.  
In order to simplify the conditions for reproducing the fault, the simple "cansend" and "candump" comand-line programs   
from "can-utils" have been used, and show the communications working between 2 Bookworm systems, and failing with the Bookworm-to-Trixie setup.  

### RPi4b set-up ###  
Install the Waveshare RS485/CAN HAT, can and can_raw drivers, and can-utils program on a Bookworm system.  
(eg see https://www.pragmaticlinux.com/2021/10/can-communication-on-the-raspberry-pi-with-socketcan)  

Use `cansend` to send a single message, which without another partner on the bus will not be ACK'd, and will repeat indefinitely.

```
cansend 555#55.55.55.55.55.55.55.55     # a regular pattern that can trigger a scope stably

```
With a bitrate of 500K, this message takes up ~200 uSec on Bookworm   
  
With the same setup on Trixie, the message takes ~265 uSec, indicating that the bitrate has not been set correctly.  

For confirmation, using `ip link show 

    
