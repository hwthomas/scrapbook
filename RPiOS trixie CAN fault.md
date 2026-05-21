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
  
With the same setup on Trixie, the message takes ~265 uSec, indicating that the bitrate is not correctl.  

For confirmation, use the command  
```
ip --details link show can0
```
The (edited) reply (on Bookworm) is...  
```
can0...
    can state ERROR-ACTIVE restart-ms 0
        bitrate 500000 sample-point 0.83
        ...
        clock 6000000 ...
```
whereas on Trixie it is...
```
can0...
    can state ERROR-ACTIVE restart-ms 0
        bitrate 500000 sample-point 0.83
        ...
        clock 8000000 ...
```
The different in clock frequency (the hardware uses the same 12MHz crystal) perhaps indicates a driver problem  



    
