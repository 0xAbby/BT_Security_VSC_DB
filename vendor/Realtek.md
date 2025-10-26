# Realtek

## Confirmed on RTL8761B(U/T)(V/E)

USB dongles confirmed to use RTL8761BU(V/E):

 * [ZEXMTE "5.4" (RTL8761B can only do 5.1!) single discrete antenna](https://amzn.to/4megB1x) ~= $16 (USB VID:DID = 0x0BDA:0x7A28) - **Recommended due to highest RSSI in my testing.**
 * [ZEXMTE "5.3" (RTL8761B can only do 5.1!) dual discrete antenna](https://amzn.to/4oswD8b) ~= $15 (USB VID:DID = 0x0BDA:0x7A29)
 * [EDUP B3536 single discrete antenna](https://amzn.to/3KSoYlf) ~= $10 (USB VID:DID = 0x2550:0x8761)
 * [TP-link UB500 single discrete antenna](https://amzn.to/4hhgZdo) ~= $18 (USB VID:DID = 0x2357:0x0604)
 * [TP-link UB500 "nano" PCB antenna](https://amzn.to/4o1sIj1) ~= $10 (USB VID:DID = 0x2357:0x0604)
 * [RTL8761BUV dev board](https://www.alibaba.com/product-detail/realtek-RTL8761BUV-dongle-Blue-tooth-development_1600150174592.html) ~= $25 (USB VID:DID = unknown, I didn't buy one.)
 * [RTL8761BTV dev board](https://www.alibaba.com/product-detail/realtek-RTL8761BTV-dongle-Blue-tooth-development_1600150205224.html) ~= $25 (USB VID:DID = N/A, UART interface)

---

### [Read Controller RAM](../type/Read_RAM.md)

VSC publicly documented by the vendor? **No**

VSC citation: Xeno's talk once public

| Functionality | OCF | Size, in bits, of memory to read (1 byte) | Address to read (4 bytes) |
| --- | --- | --- | --- |
| Read RAM | 0x061 | Valid values: 0x08, 0x10, 0x20 | Little-endian value. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 |

Scapy definition:

```
# Tested and known-working definitions
class HCI_Cmd_VSC_Realtek_Read_Mem(Packet):
    name = "Realtek Read Memory"
    fields_desc = [
        ByteField("size", 0x20),
        XLEIntField("address", 0x80000000)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Realtek_Read_Mem, ogf=0x3f, ocf=0x0061)
```

**Return parameters**:  

| Basic type | Event Code (1 byte) | Length, in bytes, of event (1 byte) | Number of Allowed Command Packets (1 byte) | Command opcode (2 bytes) | Status (1 byte) | Read data (variable, 1, 2, 4 bytes) | 
| --- | --- | --- | --- | --- | --- | --- |
| HCI Event | 0x0E (Command Complete) | 0x05 (for 1 byte read) <p> 0x06 (for 2 byte read), 0x08 (for 4 byte read)| 0x02 | 0x61, 0xFC | 0x00 = Success, <p> 0x01-0xFF = Failure | 1, 2, or 4 byte, little-endian value, depending on original size of read request. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 |

![](./file_icon.png) **Example log file!** The `.pcapng` file given [here](./Realtek_HCI_log_examples/0xfc61_VSC_Example_Read_0x8011160C-0x8011162C__USB-HCI__add_filter_"bluetooth".pcapng) shows an example of VSC 0xFC61 being used to read 0x20 bytes of memory from address 0x8011160C-0x8011162C. You can view it in Wireshark, but because the HCI transport layer is USB, you need to add a "bluetooth" filter to Wireshark to view the data more easily.

---

### [Write Controller RAM](../type/Write_RAM.md)

VSC publicly documented by the vendor? **No**

VSC citation: Xeno's talk once public

| Functionality | OCF | Size, in bits, of memory to write (1 byte) | Address to write (4 bytes) | Data to write (variable: 1, 2, 4 bytes) | 
| --- | --- | --- | --- |  --- |
| Write RAM | 0x062 | Valid values: 0x08, 0x10, 0x20 | Little-endian value. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | Little-endian value, depending on size. E.g. 0x00, 0x11, 0x22, 0x33 = 0x33221100 | 

Scapy definition:

```
# Tested and known-working definitions
class HCI_Cmd_VSC_Realtek_Write_Mem(Packet):
    name = "Realtek Write Memory"
    fields_desc = [
        ByteField("size", 0x20),
        XLEIntField("address", 0x80000000),
        XLEIntField("data_to_write", 0x33221100)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Realtek_Write_Mem, ogf=0x3f, ocf=0x0062)
```

**Return parameters**:  

| Basic type | Event Code (1 byte) | Length, in bytes, of event (1 byte) | Number of Allowed Command Packets (1 byte) | Command opcode (2 bytes) | Status (1 byte) |
| --- | --- | --- | --- | --- | --- |
| HCI Event | 0x0E (Command Complete) | 0x04 | 0x02 | 0x62, 0xFC | 0x00 = Success, <p> 0x01-0xFF = Failure |

![](./file_icon.png) **Example log file!** The `.pcapng` file given [here](./Realtek_HCI_log_examples/0xfc62_VSC_Example_Write_0x80120C00-0x80120C10__USB-HCI__add_filter_"bluetooth".pcapng) shows an example of VSC 0xFC62 being used to write 0x10 bytes of memory from address 0x80120C00-0x80120C10. You can view it in Wireshark, but because the HCI transport layer is USB, you need to add a "bluetooth" filter to Wireshark to view the data more easily.


---

### [Read Controller ROM](../type/Read_ROM.md)

VSC publicly documented by the vendor? **No**

VSC citation: Xeno's talk once public

The same VSC OCF 0x061 used above for "Read Controller RAM" can read from anywhere in the chip's memory space, and therefore can be used to read ROM (which begins at address 0x80000000) the same as it can read RAM.

---

### [Write Controller ROM Patches](../type/Write_ROM_Patches.md)

VSC publicly documented by the vendor? **No?** (but included in open source projects like Linux and Bumble.)

VSC citation: [Bumble code](https://web.archive.org/save/https://github.com/google/bumble/blob/main/bumble/drivers/rtk.py#L191), [Linux code](https://web.archive.org/web/20251020201615/https://codebrowser.dev/linux/linux/drivers/bluetooth/btrtl.c.html#rtl_download_firmware), Xeno's talk once public

| Functionality | OCF | Fragment index (1 byte) | Data to write (variable: 1-251 bytes) | 
| --- | --- | --- | --- |  --- |
| Write ROM patches (and config). | 0x020 | Which fragment this is. <p> MSBit set to 1 on the final fragment. | Up to 251 bytes of data | 

Scapy definition:

```
# Tested and known-working definitions
class HCI_Cmd_VSC_Realtek_Download_Patch(Packet):
    name = "Realtek Download Patch"
    fields_desc = [
        ByteField("index", 0x00),
        XStrLenField("data", 0, length_from=lambda pkt: pkt.underlayer.underlayer.len)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Realtek_Write_Mem, ogf=0x3f, ocf=0x0020)
```

**Return parameters**:

| Basic type | Event Code (1 byte) | Length, in bytes, of event (1 byte) | Number of Allowed Command Packets (1 byte) | Command opcode (2 bytes) | Status (1 byte) | Last fragment index (1 byte)| 
| --- | --- | --- | --- | --- | --- | --- |
| HCI Event | 0x0E (Command Complete) | 0x05 | 0x02 | 0x20, 0xFC | 0x00 = Success, <p> 0x01-0xFF = Failure | Most recently received fragment index |

![](./file_icon.png) **Example log file!** The `HCI log` file given [here](./Realtek_HCI_log_examples/0xfc20_VSC_Example_FW_Download_rtl8761bu_linux_attach.log) shows an example of the patch download which occurs naturally when an RTL8761BU-based USB dongle is attached to a Linux system. You can view it in Wireshark.

---

### [Set Bluetooth Classic / BLE Public BD_ADDR](../type/Set_BDADDR.md)

At this time there is no known VSC which can directly set the device's BD_ADDR. However, there is a "configuration file" which can achieve the same goal, which is downloaded via appending to the firmware data sent in the above "Write Controller ROM Patches" VSC OCF = 0x020.

TODO: Cite Xeno's talk about how this works in the future once it's released.