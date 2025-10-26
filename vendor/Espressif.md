# Espressif

## Confirmed on ???

Per [Espressif's reaction](https://web.archive.org/web/20250327080929/https://www.espressif.com/en/news/response_esp32_bluetooth) to the "Attacking Bluetooth the easy way" news: "These commands are present in the ESP32 chips only and are not present in any of the ESP32-C, ESP32-S, and ESP32-H series of chips."

### [Read Controller RAM](../type/Read_RAM.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña with more details [here](https://web.archive.org/web/20250811041501/https://www.tarlogic.com/blog/esp32-hidden-hci-vendor-commands/).

| Functionality | OCF | Address to read | Size, in bits, of memory element to read (1 byte) | Number of memory elements to read (variable: range?) |
| --- | --- | --- | --- | --- |
| Read RAM (`"HCI_ESP32_CMD_READ_MEM"`) | 0x001 | Little-endian value. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | Valid values: 0x08, 0x10, 0x20 | Valid range: ? | 

Scapy definition:

```
# Untested definition
class HCI_Cmd_VSC_Espressif_Read_Mem(Packet):
    name = "Espressif Read Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000)
        ByteField("element_size", 0x20),
        ByteField("num_elements", 0x01),
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Espressif_Read_Mem, ogf=0x3f, ocf=0x0001)
```

**Return parameters**:

| Basic type | Event Code (1 byte) | Length, in bytes, of event (1 byte) | Number of Allowed Command Packets (1 byte) | Command opcode (2 bytes) | Status (1 byte) | Number of memory elements returned (1 byte) | Read data (variable: range?) | 
| --- | --- | --- | --- | --- | --- | --- | --- |
| HCI Event | 0x0E (Command Complete) | (variable: range?) | 0x02(?) | 0x01, 0xFC | 0x00 = Success, <p> 0x01-0xFF = Failure | 1, 2, or 4 byte, little-endian value, depending on original size of read request. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | Data read from the controller. (FIXME: is it all little-endian?) |


---

### [Write Controller RAM](../type/Write_RAM.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña with more details [here](https://web.archive.org/web/20250811041501/https://www.tarlogic.com/blog/esp32-hidden-hci-vendor-commands/).

| Functionality | OCF | Address to write (4 bytes) | Size, in bits, of memory element to read (1 byte) | Number of memory elements to read (variable: range?) | Data to write (variable: range?) | 
| --- | --- | --- | --- | --- | --- |
| Write RAM | 0x002 | Little-endian value. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | Valid values: 0x08, 0x10, 0x20 | Valid range: ? | Data to write to the controller. (FIXME: is it all little-endian?) |

Scapy definition:

```
# Tested and known-working definitions
class HCI_Cmd_VSC_Espressif_Write_Mem(Packet):
    name = "Espressif Write Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000),
        ByteField("element_size", 0x20),
        ByteField("num_elements", 0x01),
        XLEIntField("data_to_write", 0x33221100)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Espressif_Write_Mem, ogf=0x3f, ocf=0x0002)
```

**Return parameters**:  

| Basic type | Event Code (1 byte) | Length, in bytes, of event (1 byte) | Number of Allowed Command Packets (1 byte) | Command opcode (2 bytes) | Status (1 byte) |
| --- | --- | --- | --- | --- | --- |
| HCI Event | 0x0E (Command Complete) | 0x04 | 0x02 | 0x62, 0xFC | 0x00 = Success, <p> 0x01-0xFF = Failure |

---

### [Read Controller Non-volatile Memory (e.g. SPI NOR Flash)](../type/Read_NVM.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña.

| Functionality | OCF | Size of memory to read (in ?)? | Address to read |
| --- | --- | --- | --- |
| Read Non-volatile Memory | 0x007 | {valid values: ???} | ??? |

Scapy definition:

```
TODO
```

---

### [Write Controller Non-volatile Memory (e.g. SPI NOR Flash)](../type/Write_NVM.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña  

| Functionality | OCF | Size of memory to read (in ?)? | Address to read |
| --- | --- | --- | --- |
| Write Non-volatile Memory | 0x008 | {valid values: ???} | ??? |

Scapy definition:

```
TODO
```

---

### [Read Controller ROM](../type/Read_ROM.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña  

Can VSC 0x001 be used?

---

### [Read Controller Registers](../type/Read_Regs.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña  

VSC 0x030 TODO

---

### [Write Controller Registers](../type/Write_Regs.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña  

VSC 0x031 TODO

---

### [Set Bluetooth Classic / BLE Public BD_ADDR](../type/Set_BDADDR.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña with more details [here](https://web.archive.org/web/20250811041501/https://www.tarlogic.com/blog/esp32-hidden-hci-vendor-commands/).  

| Functionality | OCF | BD_ADDR (6 bytes) |
| --- | --- | --- | 
| Set BDADDR (`"HCI_ESP32_CMD_SET_MAC"`)| 0x032 | Little-endian value. E.g. 0x12, 0x34, 0x56, 0x78, 0x90, 0xab = 0xab9078563412. |

Scapy definition:

```
class HCI_Cmd_VSC_Espressif_Write_BDADDR(Packet):
    name = "Espressif Write BDADDR"
    fields_desc = [
        BDAddrField("bdaddr", None)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Espressif_Write_BDADDR, ogf=0x3f, ocf=0x0032)
```

**Return parameters**:

| Basic type | Event Code (1 byte) | Length, in bytes, of event (1 byte) | Number of Allowed Command Packets (1 byte) | Command opcode (2 bytes) | Status (1 byte) |
| --- | --- | --- | --- | --- | --- |
| HCI Event | 0x0E (Command Complete) | 0x04 | 0x02 | 0x32, 0xFC | 0x00 = Success, <p> 0x01-0xFF = Failure |

---

### [Send arbitrary LMP packets](../type/Send_LMP.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña  

VSC 0x00E TODO

---

### [Send arbitrary LLCP packets](../type/Send_LLCP.md)

VSC publicly documented by the vendor? **No**

VSC citation: [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña  

VSC 0x043 TODO