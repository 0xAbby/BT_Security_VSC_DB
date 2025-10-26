# Cypress

## *Unconfirmed* on CYW43XX

Per [the documentation](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce) all 
the below VSCs should apply to CYW43XX chips.

### [Set Bluetooth Classic / BLE Public BD_ADDR](../type/Set_BDADDR.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce)

| Functionality | OCF | Power value (encoded) (6 bytes) |
| --- | --- | --- |
| Set BD_ADDR (`"Write_BD_ADDR"`) | 0x001 | 6 byte, little-endian value. E.g. 0x12, 0x34, 0x56, 0x78, 0x90, 0xab = 0xab9078563412} |

Scapy definition:

```
# NOTE: Untested definition
class HCI_Cmd_VSC_Cypress_Write_BDADDR(Packet):
    name = "Cypress Write BDADDR"
    fields_desc = [
        BDAddrField("bdaddr", None)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Cypress_Write_BDADDR, ogf=0x3f, ocf=0x0001)
```

**Return parameters**:

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) |
| --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure |

---

## Confirmed on CYW4339

The [InternalBlue](https://darkmentor.com/bt.html#InternalBlue%20a%20Bluetooth%20Experimentation%20Framework%20Based%20on%20Mobile%20Device%20Reverse%20Engineering) masters thesis by Dennis Mantz originally did the work on the BCM4339/CYW4339 chip, and confirmed the below VSCs' presence.

### [Write Controller RAM](../type/Write_RAM.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce)

| Functionality | OCF   | Address to write (4 bytes) | Data to write (variable: 1-251 bytes)|
| --- | --- | --- | --- |  --- |
| Write RAM (`"Write_RAM"`) | 0x04C | Little-endian value. <p> E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | Byte array of data to write, up to 251 bytes | 

Scapy definition:

```
# NOTE: Untested definition
class HCI_Cmd_VSC_Cypress_Write_Mem(Packet):
    name = "Cypress Write Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000),
        PacketListField("data_to_write", [], HCI_Command_Hdr,
                         length_from=lambda pkt: pkt.size) # FIXME: what is the right way to represent a byte array where the size is not given by a size variable?
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Cypress_Write_Mem, ogf=0x3f, ocf=0x004c)
```

**Return parameters**:

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) |
| --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure |

---

### [Read Controller RAM](../type/Read_RAM.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce)

| Functionality | OCF   | Address to read (4 bytes) | Size, in bytes, of memory to read (1 byte) |
| --- | --- | --- | --- |
| Read RAM (`"Read_RAM"`) | 0x04D | 4 byte, little-endian value. <p> E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | Valid values: 1-251 |

Scapy definition:

```
# NOTE: Untested definition
class HCI_Cmd_VSC_Cypress_Read_Mem(Packet):
    name = "Cypress Read Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000),
        ByteField("size", 0x20)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Cypress_Read_Mem, ogf=0x3f, ocf=0x004d)
```

**Return parameters**:

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) | Read data (variable: 1-251 bytes)|
| --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure | Up to 251 bytes of data |

---

### [Write Controller ROM Patches](../type/Write_ROM_Patches.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce)

The below `"Write_RAM"` command is intended to be used after the `"Download_Minidriver"` to write patches (but `"Write_RAM"` can actually be used at other times as well.)

| Functionality | OCF | Parameters N/A |
| --- | --- | --- |
| Reset device to prepare for ROM patches (`"Download_Minidriver"`) | 0x02e | No parameters, because it just "triggers the device to reboot into a state where it is prepared to receive a download of a minidriver." |

Scapy definition:

```
# NOTE: Untested definition
class HCI_Cmd_VSC_Cypress_Download_Minidriver(Packet):
    name = "Cypress Download Minidriver"
    fields_desc = [
        # FIXME how to specify there are no arguments?
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Cypress_Read_Mem, ogf=0x3f, ocf=0x002e)
```

---
**Related:**

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce)

Documentation explanation of intended usage:

```
The commands Jumps into the target address in Thumb mode, typically a minidriver entry point, or in the case of an 0xFFFFFFFF target address, an implied Bluetooth mode reentry vector with acceptance of runtime RAM configuration data. This command is primarily intended to vector from firmware in Download mode (having received a Download_Minidriver vendor-specific HCI command) into a minidriver, which has just been received, to reset the device by jumping to the reset vector when the minidriver is no longer needed, or in the case of an 0xFFFFFFFF target address, to transition from Download mode back to Bluetooth mode with acceptance of configuration data which was downloaded by Write_RAM vendor-specific HCI commands.
```

| Functionality | OCF | Address to execute (4 bytes) |
| --- | --- | --- |
| Execute code at given address (`"Launch_RAM"`) | 0x04e | Little-endian value. <p> E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 |

Scapy definition:

```
# NOTE: Untested definition
class HCI_Cmd_VSC_Cypress_Launch_RAM(Packet):
    name = "Cypress launch code at RAM address"
    fields_desc = [
        XLEIntField("address", 0x80000000)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Cypress_Launch_RAM, ogf=0x3f, ocf=0x004e)
```