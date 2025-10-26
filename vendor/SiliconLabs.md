# Silicon Labs

## *Unconfirmed* on EFR32* chips

(Note: Per the [documentation](https://web.archive.org/web/20250912020532/https://www.silabs.com/documents/public/application-notes/an1328-enabling-rcp-using-bt-hci.pdf) these VSCs should apply to [EFR32](https://www.silabs.com/wireless/bluetooth) chips.

---

### [Set TX power level](../type/Set_TX_Power.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20251020114425/https://software-dl.ti.com/simplelink/esd/simplelink_cc13x2_26x2_sdk/2.40.00.81/exports/docs/ble5stack/vendor_specific_guide/BLE_Vendor_Specific_HCI_Guide/hci_cmd_extracted.html)


| Functionality | OCF | Minimum power (dBm) |  Maximum power (dBm) |
| --- | --- | --- | --- |
| Set (minimum & maximum) TX Power (in dBm) (`"HCI_VS_Silabs_Set_Min_Max_TX_Power"`) | 0x014 | 2 bytes, value in dBm. Minimum acceptable TX power. But valid values are defined per-chip and must be looked up with `HCI_VS_SiliconLabs_Read_Current_TX_Power_Configuration` | 2 bytes, value in dBm. Maximum acceptable TX power. But valid values are defined per-chip and must be looked up with `HCI_VS_SiliconLabs_Read_Current_TX_Power_Configuration` | 

Scapy definition:

```
class HCI_Cmd_VSC_SiLabs_Set_TX_Power(Packet):
    name = "Silicon Labs Set Minimum & Maximum TX Power"
    fields_desc = [
        XLEShortField("min_tx_power", 0x00)
        XLEShortField("max_tx_power", 0x00)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_SiLabs_Set_TX_Power, ogf=0x3f, ocf=0x0014)
```

**Return parameters**:

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) |
| --- |
| 0 = Success, <p> 0x01-0xFF = Failure |

---
**Related:**

| Functionality | OCF | Parameters N/A |
| --- | --- | --- |
| Check chip-specific minimum & maximum TX Power (in dBm) (`"HCI_VS_SiliconLabs_Read_Current_TX_Power_Configuration"`) | 0x017 | No parameters (it just returns values) | 

Scapy definition:

```
class HCI_Cmd_VSC_SiLabs_Get_Supported_TX_Power(Packet):
    name = "Silicon Labs Get Minimum & Maximum TX Power"
    fields_desc = [
        # FIXME: how do we represent something with no data fields?
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_SiLabs_Set_TX_Power, ogf=0x3f, ocf=0x0017)
```

**Return parameters**:

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) | `min_supported_tx_power` (2 bytes) | `max_supported_tx_power` (2 bytes) | `min_configured_tx_power` (2 bytes) | `max_configured_tx_power` (2 bytes) | `tx_rf_path_compensation` |
| --- | --- | --- | --- | --- | --- |
| 0 = Success, <p> 0x01-0xFF = Failure | Minimum TX power supported by the radio. The unit is deci-dBm. | Maximum TX power supported by the radio. The unit is deci-dBm | Minimum TX power configured to be used. The unit is in deci-dBm and value must be within the range `min_supported_tx_power` - `max_supported_tx_power`. | Maximum TX power configured to be used. The unit is in deci-dBm and value must be within the range `min_supported_tx_power`—`max_supported_tx_power`. | Currently configured TX RF path compensation in deci-dBms |

---
**Related:**

| Functionality | OCF | Connection handle (2 bytes) | TX power (2 bytes) |
| --- | --- | --- | --- |
| Set TX Power (in deci-dBm) on a per-connection basis (`"HCI_VS_Siliconlabs_Set_Connection_Tx_Power"`) | 0x030 | Little-endian, connection handle (received from HCI layer on connection success.) | Little-endian TX power (in deci-dBm) |

```
class HCI_Cmd_VSC_SiLabs_Set_Connection_TX_Power(Packet):
    name = "Silicon Labs set TX power for specific connection"
    fields_desc = [
        XLEShortField("connection_handle", 0x0001)
        XLEShortField("tx_power", 0x0000)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_SiLabs_Set_Connection_TX_Power, ogf=0x3f, ocf=0x0030)
```

**Return parameters**:

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) |
| --- |
| 0 = Success, <p> 0x01-0xFF = Failure |

---

### [Set Bluetooth Classic / BLE Public BD_ADDR](../type/Set_BDADDR.md)

VSC publicly documented by the vendor? **Yes**

VSC citation: [here](https://web.archive.org/web/20250912020532/https://www.silabs.com/documents/public/application-notes/an1328-enabling-rcp-using-bt-hci.pdf)

| Functionality | OCF | BD_ADDR (6 bytes) |
| --- | --- | --- | 
| Set BDADDR (`"HCI_VS_SiliconLabs_Set_Public_Address"`)| 0x028 | Little-endian value. E.g. 0x12, 0x34, 0x56, 0x78, 0x90, 0xab = 0xab9078563412. <p> (If NULL, device-specific address is used.) |

Scapy definition:

```
class HCI_Cmd_VSC_SiLabs_Write_BDADDR(Packet):
    name = "Silicon Labs Write BDADDR"
    fields_desc = [
        BDAddrField("bdaddr", None)
    ]

bind_layers(HCI_Command_Hdr, HCI_Cmd_VSC_SiLabs_Write_BDADDR, ogf=0x3f, ocf=0x0028)
```

**Return parameters**:

(Currently unknown what kind of VSE this comes back in.)

| Status (1 byte) |
| --- |
| 0 = Success, <p> 0x01-0xFF = Failure |

---