# Broadcom

## Confirmed on multiple Broadcom chips

The [InternalBlue](https://darkmentor.com/bt.html#InternalBlue%20a%20Bluetooth%20Experimentation%20Framework%20Based%20on%20Mobile%20Device%20Reverse%20Engineering) masters thesis by Dennis Mantz originally did the work on the BCM4339/CYW4339 chip. However the [InternalBlue code](https://github.com/seemoo-lab/internalblue/blob/master/doc/firmware.md) lists many more potentially-applicable Broadcom chips, but indicates "we only have firmware information on a subset of these". The chips for which we can reasonably believe the VSCs have been confirmed, are those for which a firmware file exists in [this directory](https://github.com/seemoo-lab/internalblue/tree/master/internalblue/fw).

---

### [Write Controller RAM](../type/Write_RAM.md)

VSC publicly documented by the vendor? **No**

VSC citation: [InternalBlue](https://darkmentor.com/bt.html#InternalBlue%20a%20Bluetooth%20Experimentation%20Framework%20Based%20on%20Mobile%20Device%20Reverse%20Engineering) masters thesis by Dennis Mantz which utilized [Cypress documentation](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce)


| Functionality | OCF   | Address to write (4 bytes) | Data to write (variable: 1-251 bytes)|
| --- | --- | --- | --- |  --- |
| Write RAM (`"Write_RAM"`) | 0x04C | Little-endian value. <p> E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | Byte array of data to write, up to 251 bytes | 

Scapy definition:

```
# NOTE: Untested definition
class HCI_Cmd_VSC_Broadcom_Write_Mem(Packet):
    name = "Broadcom Write Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000),
        PacketListField("data_to_write", [], HCI_Command_Hdr,
                         length_from=lambda pkt: pkt.size) # FIXME: what is the right way to represent a byte array where the size is not given by a size variable?
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Broadcom_Write_Mem, ogf=0x3f, ocf=0x004c)
```

**Return parameters**:

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) |
| --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure |

---

### [Read Controller RAM](../type/Read_RAM.md)

VSC publicly documented by the vendor? **No**

VSC citation: [InternalBlue](https://darkmentor.com/bt.html#InternalBlue%20a%20Bluetooth%20Experimentation%20Framework%20Based%20on%20Mobile%20Device%20Reverse%20Engineering) masters thesis by Dennis Mantz which utilized [Cypress documentation](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce)

| Functionality | OCF   | Address to read (4 bytes) | Size, in bytes, of memory to read (1 byte) |
| --- | --- | --- | --- |
| Read RAM (`"Read_RAM"`) | 0x04D | 4 byte, little-endian value. <p> E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | Valid values: 1-251 |

Scapy definition:

```
# NOTE: Untested definition
class HCI_Cmd_VSC_Broadcom_Read_Mem(Packet):
    name = "Broadcom Read Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000),
        ByteField("size", 0x20)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Broadcom_Read_Mem, ogf=0x3f, ocf=0x004d)
```

**Return parameters**:

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) | Read data (variable: 1-251 bytes)|
| --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure | Up to 251 bytes of data |

---

### [Write Controller ROM Patches](../type/Write_ROM_Patches.md)

VSC publicly documented by the vendor? **No**

VSC citation: [InternalBlue](https://darkmentor.com/bt.html#InternalBlue%20a%20Bluetooth%20Experimentation%20Framework%20Based%20on%20Mobile%20Device%20Reverse%20Engineering) masters thesis by Dennis Mantz which utilized [Cypress documentation](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce)

The below `"Write_RAM"` command is intended to be used after the `"Download_Minidriver"` to write patches (but `"Write_RAM"` can actually be used at other times as well.)

| Functionality | OCF | Parameters N/A |
| --- | --- | --- |
| Reset device to prepare for ROM patches (`"Download_Minidriver"`) | 0x02e | No parameters, because it just "triggers the device to reboot into a state where it is prepared to receive a download of a minidriver." |

Scapy definition:

```
# NOTE: Untested definition
class HCI_Cmd_VSC_Broadcom_Download_Minidriver(Packet):
    name = "Broadcom Download Minidriver"
    fields_desc = [
        # FIXME how to specify there are no arguments?
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Broadcom_Read_Mem, ogf=0x3f, ocf=0x002e)
```

---
**Related:**

VSC publicly documented by the vendor? **No**

VSC citation: [InternalBlue](https://darkmentor.com/bt.html#InternalBlue%20a%20Bluetooth%20Experimentation%20Framework%20Based%20on%20Mobile%20Device%20Reverse%20Engineering) masters thesis by Dennis Mantz which utilized [Cypress documentation](https://web.archive.org/web/20251020121706/https://community.infineon.com/gfawx74859/attachments/gfawx74859/WifiBTcombo/955/1/cypress%20vendor%20specific%20commands.pdf?nobounce)

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
class HCI_Cmd_VSC_Broadcom_Launch_RAM(Packet):
    name = "Broadcom launch code at RAM address"
    fields_desc = [
        XLEIntField("address", 0x80000000)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_Broadcom_Launch_RAM, ogf=0x3f, ocf=0x004e)
```

---

### [Set Bluetooth Classic / BLE Public BD_ADDR](../type/Set_BDADDR.md)

InternalBlue didn't discuss the `"Write_BD_ADDR"` VSC that is present in Cypress' documentation. However it is reasonable to believe it will exist on the same chips that share the above VSCs. For more information see our [Cypress](./Cypress.md) page.
