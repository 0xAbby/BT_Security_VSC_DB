# Cambridge Silicon Radio (CSR)

## Confirmed on "CSR 4.0" dongle (CSR8510 chip according to vendor)

* ["CSR 4.0" dongle](https://amzn.to/49fd92r) ~= $7 (USB VID:DID = 0a12:0001)

### [Set Bluetooth Classic / BLE Public BD_ADDR](../type/Set_BDADDR.md)

VSC publicly documented by the vendor? **No**

VSC citation: [here](https://web.archive.org/web/20250929011708/https://github.com/bluez/bluez/blob/master/tools/bdaddr.c#L102)

| Functionality | OCF | Strange encoding | 
| --- | --- | --- |
| Set BD_ADDR (`"Write_BD_ADDR"`) | 0x000 | cmd[] = {0x02, 0x00, 0x0c, 0x00, 0x11, 0x47, 0x03, 0x70, 0x00, 0x00, 0x01, 0x00, 0x04, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00 }, where the bdaddr bytes are inserted as <p> cmd[16] = bdaddr->b[2];<br>cmd[17] = 0x00;<br>cmd[18] = bdaddr->b[0];<br>cmd[19] = bdaddr->b[1];<br>cmd[20] = bdaddr->b[3];<br>cmd[21] = 0x00;<br>cmd[22] = bdaddr->b[4];<br>cmd[23] = bdaddr->b[5];|

**Return parameters**:  
*TODO*

Scapy definition:

```
TODO
```

