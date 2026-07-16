### Integrating asyncio and non-asyncio code ###  
I am trying to combine two python 3 programs, one of which is structured as an infinite loop calling a number of sections which are programmed with non-blocking calls to (for example) CAN-bus kernel drivers, and the other making asyncio calls using ble-serial to read from an OBDII dongle.  

The non-asyncio code is typical of industrial Programmable Logic Controller (PLC) systems, with structure :-  

```
while(True):
    # read hardware inputs into memory image
    # process a series of logic statements to produce a memory image of all hardware outputs
    # write memory image to hardware outputs
    time.sleep(scan_time)    # sleep before rescanning inputs, etc
