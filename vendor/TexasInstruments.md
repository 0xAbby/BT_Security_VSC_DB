# Texas Instruments

## Confirmed on WL1835MOD

(Note: Per the [documentation](https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf) these VSCs should apply to "WiLink™ 8.0 Bluetooth® firmware" which is applicable to chips WL1831MOD, WL1835MOD, WL1837MOD (WL183XMOD) and "WiLink 8Q (automotive) including WL183xQ and WL187xQ".

---

### [Read Controller Registers](../type/Read_Regs.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf](https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf)


| Functionality | OCF | Address to read | 
| --- | --- | --- |
| Read Registers (`"HCI_VS_Read_Hardware_Register"`) | 0x300 | 4 byte, little-endian value. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 |

Scapy definition:

```
class HCI_Cmd_VSC_TI_Read_HW_Regs(Packet):
    name = "Texas Instruments Read Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_TI_Read_HW_Regs, ogf=0x3f, ocf=0x0300)
```

**Return parameters**:  

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) | Memory value (2 bytes) |
| --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure | Little-endian register contents|

---

### [Write Controller Registers](../type/Write_Regs.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf](https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf)

| Functionality | OCF | Address to read | Value to write | 
| --- | --- | --- | --- |
| Write Registers (`"HCI_VS_Write_Hardware_Register"`) | 0x301 | 4 byte, little-endian value. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | 2 byte, little-endian value. E.g. 0x11, 0x22 = 0x2211 |

Scapy definition:

```
class HCI_Cmd_VSC_TI_Write_HW_Regs(Packet):
    name = "Texas Instruments Read Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000),
        XLEShortField("data_to_write", 0x1234)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_TI_Write_HW_Regs, ogf=0x3f, ocf=0x0301)
```

**Return parameters**:  

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) |
| --- |
| 0 = Success, <p> 0x01-0xFF = Failure |

---

### [Read Controller RAM](../type/Read_RAM.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf](https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf)


| Functionality | OCF | Address to read | Size of memory to read (in bytes) | 
| --- | --- | --- | --- |
| Read RAM (`"HCI_VS_Read_Memory"`) | 0x302 | 4 byte, little-endian value. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412 | Valid values: 0x01, 0x02, 0x04 |

Scapy definition:

```
class HCI_Cmd_VSC_TI_Read_Mem(Packet):
    name = "Texas Instruments Read Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000),
        ByteField("size", 0x04)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_TI_Read_Mem, ogf=0x3f, ocf=0x0302)
```

**Return parameters**:  

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) | Memory value (1, 2, 4 bytes) |
| --- | --- | --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure | {Little-endian memory contents }|

---

### [Write Controller RAM](../type/Write_RAM.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf](https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf)

| Functionality | OCF | Address to write | Size of memory to write (in bytes) | Data to write | 
| --- | --- | --- | --- | --- |
| Write RAM (`"HCI_VS_Write_Memory"`) | 0x303 | 4 byte, little-endian value. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412} | Valid values: 0x01, 0x02, 0x04 | Always a 4 byte, little-endian value. E.g. 0x12, 0x34, 0x56, 0x78 = 0x78563412, but 1 or 2 most-significant bytes are ignored if size is less than 4. |

Scapy definition:

```
class HCI_Cmd_VSC_TI_Write_Mem(Packet):
    name = "Texas Instruments Write Memory"
    fields_desc = [
        XLEIntField("address", 0x80000000),
        ByteField("size", 0x20),
        XLEIntField("data_to_write", 0x33221100)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_TI_Write_Mem, ogf=0x3f, ocf=0x0303)
```

**Return parameters**:  

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) |
| --- |
| 0 = Success, <p> 0x01-0xFF = Failure |

---

### [Read Controller ROM](../type/Read_ROM.md)

The same VSC OCF 0x302 used above for "Read Controller RAM" can read from anywhere in the chip's memory space, and therefore can be used to read ROM the same as it can read RAM.

---

### [Set Bluetooth Classic / BLE Public BD_ADDR](../type/Set_BDADDR.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf](https://web.archive.org/web/20250415184223/https://www.ti.com/lit/ug/swru442b/swru442b.pdf)

| Functionality | OCF | BD_ADDR | 
| --- | --- | --- | 
| Set BDADDR (`"HCI_VS_Write_BD_Addr"`)| 0x006 | 6 byte, little-endian value. E.g. 0x12, 0x34, 0x56, 0x78, 0x90, 0xab = 0xab9078563412} |

Scapy definition:

```
class HCI_Cmd_VSC_TI_Write_BDADDR(Packet):
    name = "Texas Instruments Write BDADDR"
    fields_desc = [
        BDAddrField("bdaddr", None)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_TI_Write_BDADDR, ogf=0x3f, ocf=0x0006)
```

**Return parameters**:  

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) |
| --- |
| 0 = Success, <p> 0x01-0xFF = Failure |

---
---

## *Unconfirmed* on cc13x2 & cc254x & cc26xx

Per [this documentation](https://web.archive.org/web/20251020111601/https://software-dl.ti.com/simplelink/esd/simplelink_cc13x2_26x2_sdk/2.40.00.81/exports/docs/ble5stack/vendor_specific_guide/BLE_Vendor_Specific_HCI_Guide/hci_interface.html) the below interfaces should be available on TI CC13X2 / CC254X / CC26XX chips.

---

### [Set TX power level](../type/Set_TX_Power.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020114425/https://software-dl.ti.com/simplelink/esd/simplelink_cc13x2_26x2_sdk/2.40.00.81/exports/docs/ble5stack/vendor_specific_guide/BLE_Vendor_Specific_HCI_Guide/hci_cmd_extracted.html)

| Functionality | OCF | Power value (encoded) | 
| --- | --- | --- |
| Set TX Power (in dBm) (`"HCI_EXT_SetTxPowerCmd"`) | 0x001 | 1 byte, possible values 0-27, see documentation for per-chip interpretations. | 

Scapy definition:

```
class HCI_Cmd_VSC_TI2_Set_TX_Power(Packet):
    name = "Texas Instruments Set TX Power"
    fields_desc = [
        ByteField("power_encoded", 0x00)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_TI2_Set_TX_Power, ogf=0x3f, ocf=0x0001)
```


**Return parameters**:  

(Currently unknown what kind of VSE this comes back in.)

`HCI_EXT_SetTxPowerDone`

| Status (1 byte) | Command opcode | 
| --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure | 0x01, 0xFC | 

---

### [Set Bluetooth Classic / BLE Public BD_ADDR](../type/Set_BDADDR.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020114425/https://software-dl.ti.com/simplelink/esd/simplelink_cc13x2_26x2_sdk/2.40.00.81/exports/docs/ble5stack/vendor_specific_guide/BLE_Vendor_Specific_HCI_Guide/hci_cmd_extracted.html)


| Functionality | OCF | Power value (encoded) | 
| --- | --- | --- |
| Set BD_ADDR (`"HCI_EXT_SetBDADDRCmd"`) | 0x00C | 6 byte, little-endian value. E.g. 0x12, 0x34, 0x56, 0x78, 0x90, 0xab = 0xab9078563412} |

Scapy definition:

```
class HCI_Cmd_VSC_TI2_Write_BDADDR(Packet):
    name = "Texas Instruments Write BDADDR"
    fields_desc = [
        BDAddrField("bdaddr", None)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_TI2_Write_BDADDR, ogf=0x3f, ocf=0x000c)
```

**Return parameters**:  

(Currently unknown what kind of VSE this comes back in.)

`HCI_EXT_SetBDADDRDone`

| Status (1 byte) | Command opcode | 
| --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure | 0x0C, 0xFC | 

---

### [Read Controller Non-volatile Memory (e.g. SPI NOR Flash)](../type/Read_NVM.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020113153/https://software-dl.ti.com/simplelink/esd/simplelink_cc13x2_26x2_sdk/2.40.00.81/exports/docs/ble5stack/vendor_specific_guide/BLE_Vendor_Specific_HCI_Guide/util_api.html)

| Functionality | OCF | nvID to read | Size of memory to read (in bytes?) | 
| --- | --- | --- | --- |
| Read RAM (`"UTIL_NV_Read"`) | 0x281 | 1 byte | Valid values: any? |

Scapy definition:

```
class HCI_Cmd_VSC_TI2_Read_NVM(Packet):
    name = "Texas Instruments Read Non-Volatile Memory by nvID"
    fields_desc = [
        ByteField("nvID", 0x00),
        ByteField("size", 0x01)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_TI2_Read_NVM, ogf=0x3f, ocf=0x0281)
```

**Return parameters**:  

*TODO* Unknown.

---

### [Write Controller Non-volatile Memory (e.g. SPI NOR Flash)](../type/Write_NVM.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020113153/https://software-dl.ti.com/simplelink/esd/simplelink_cc13x2_26x2_sdk/2.40.00.81/exports/docs/ble5stack/vendor_specific_guide/BLE_Vendor_Specific_HCI_Guide/util_api.html)


| Functionality | OCF | nvID to write | Size of memory to write (in bytes?) | Data to write |
| --- | --- | --- | --- | --- |
| Read RAM (`"UTIL_NV_Write"`) | 0x282 | 1 byte | Valid values: any? | 1 byte |

Scapy definition:

```
class HCI_Cmd_VSC_TI2_Write_NVM(Packet):
    name = "Texas Instruments Write Non-Volatile Memory by nvID"
    fields_desc = [
        ByteField("nvID", 0x00),
        ByteField("size", 0x01),
        ByteField("data_to_write", 0x01)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_TI2_Write_NVM, ogf=0x3f, ocf=0x0282)
```

**Return parameters**:  

*TODO* Unknown.

