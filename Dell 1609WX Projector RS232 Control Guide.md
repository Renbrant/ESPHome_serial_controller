# Dell 1609WX Projector RS232 Control Guide

This repository provides the technical documentation and command set for controlling the **Dell 1609WX Projector** via serial RS232 communication.

---

## 1. Hardware Interface

### Connector Type
The projector uses a **Mini DIN-6** connector. Since most PCs use a DB9 connector, you will need an adapter cable.

| Signal | Description | Mini DIN-6 Pin |
| :--- | :--- | :--- |
| **TXD** | Transmit Data | 5 |
| **RXD** | Receive Data | 3 |
| **GND** | Ground | 1, 2 |

### Serial Port Settings
Configure your communication terminal (e.g., PuTTY, Tera Term, or custom script) with these settings:
* **Baud Rate**: 19200 bps
* **Data Bits**: 8 bits
* **Parity**: None
* **Stop Bits**: 1 bit
* **Flow Control**: None

---

## 2. Protocol Format

The protocol uses a specific binary hex structure. Multi-byte values are sent in **Little-Endian** format (Low Byte first).

**Packet Structure:**
`[Header] [Address] [Payload Size] [CRC16] [MsgID] [MsgSize] [Command] [Value]`

* **Header**: Fixed at `0xBE, 0xEF`.
* **Address**: Fixed at `0x10`.
* **CRC16**: Checksum (calculated for the packet).
* **MsgID**: Fixed at `0x11, 0x11`.

---

## 3. Command Reference

The hex strings below are ready-to-send packets including the header and checksum.

### System Control
| Command | Hex Data String |
| :--- | :--- |
| **Power On** | `be ef 10 05 00 c6 ff 11 11 01 00 01` |
| **Power Off** | `be ef 10 05 00 0c 3e 11 11 01 00 18` |
| **Menu** | `be ef 10 05 00 c7 bf 11 11 01 00 02` |
| **Enter** | `be ef 10 05 00 f6 3f 11 11 01 00 40` |
| **Up** | `be ef 10 05 00 07 7e 11 11 01 00 03` |
| **Down** | `be ef 10 05 00 c5 3f 11 11 01 00 04` |
| **Left** | `be ef 10 05 00 05 fe 11 11 01 00 05` |
| **Right** | `be ef 10 05 00 04 be 11 11 01 00 06` |

### Input Source Selection
| Source | Hex Data String |
| :--- | :--- |
| **VGA Analog 1** | `be ef 10 05 00 cc ff 11 11 01 00 19` |
| **VGA Analog 2** | `be ef 10 05 00 28 fe 11 11 01 00 69` |
| **DVI** | `be ef 10 05 00 3a 3e 11 11 01 00 50` |
| **S-Video** | `be ef 10 05 00 1f be 11 11 01 00 22` |
| **Composite Video** | `be ef 10 05 00 df 7f 11 11 01 00 23` |

### Audio and Image
| Command | Hex Data String |
| :--- | :--- |
| **Volume +** | `be ef 10 05 00 00 fe 11 11 01 00 09` |
| **Volume -** | `be ef 10 05 00 01 be 11 11 01 00 0a` |
| **Mute (Toggle)** | `be ef 10 05 00 c3 ff 11 11 01 00 0d` |
| **Mute Off** | `be ef 10 05 00 3c 98 11 11 01 00 5f` |
| **Blank Screen (Hide)** | `be ef 10 05 00 02 7e 11 11 01 00 0f` |
| **Eco Mode On** | `be ef 10 05 00 d9 bf 11 11 01 00 2a` |
| **Eco Mode Off** | `be ef 10 05 00 19 7e 11 11 01 00 2b` |

---

## 4. Response Messages

The projector will respond with a status code for every command sent.

| Status Byte | Meaning |
| :--- | :--- |
| **0x00** | Success |
| **0x01** | Invalid Command (Valid but not available now) |
| **0x02** | Error Command (CRC error or unknown) |

### Status Queries
To read the current state, send the following query:
* **System Status Query**: `be ef 10 05 00 46 7e 11 11 01 00 ff`
    * Response Byte 2: `0x01` (Standby), `0x02` (Warm Up), `0x03` (On), `0x04` (Cooling).

---
*Based on Dell 1609WX RS232 Protocol Specifications, 2008.*


# Comandos de Controlo - Dell 1609WX

| Comando | Pacote Hexadecimal (Little-Endian) |
| :--- | :--- |
| Power (On/Off Toggle) | be ef 10 05 00 c6 ff 11 11 01 00 01 |
| Menu | be ef 10 05 00 c7 bf 11 11 01 00 02 |
| Up | be ef 10 05 00 07 7e 11 11 01 00 03 |
| Down | be ef 10 05 00 c5 3f 11 11 01 00 04 |
| Left | be ef 10 05 00 05 fe 11 11 01 00 05 |
| Right | be ef 10 05 00 04 be 11 11 01 00 06 |
| R-sync | be ef 10 05 00 c4 7f 11 11 01 00 07 |
| Source (Toggle) | be ef 10 05 00 c0 3f 11 11 01 00 08 |
| Volume + | be ef 10 05 00 00 fe 11 11 01 00 09 |
| Volume - | be ef 10 05 00 01 be 11 11 01 00 0a |
| Zoom In | be ef 10 05 00 c1 7f 11 11 01 00 0b |
| Zoom Out | be ef 10 05 00 03 3e 11 11 01 00 0c |
| Mute | be ef 10 05 00 c3 ff 11 11 01 00 0d |
| Hide (Blank Screen) | be ef 10 05 00 02 7e 11 11 01 00 0f |
| Video Mode | be ef 10 05 00 ca 3f 11 11 01 00 10 |
| V. Keystone Up | be ef 10 05 00 cb 7f 11 11 01 00 13 |
| V. Keystone Down | be ef 10 05 00 09 3e 11 11 01 00 14 |
| Aspect Ratio (Toggle) | be ef 10 05 00 08 7e 11 11 01 00 17 |
| Power Off (Forçado) | be ef 10 05 00 0c 3e 11 11 01 00 18 |
| Source-VGA Analog 1 | be ef 10 05 00 cc ff 11 11 01 00 19 |
| Source-S-Video | be ef 10 05 00 1f be 11 11 01 00 22 |
| Source-Composite | be ef 10 05 00 df 7f 11 11 01 00 23 |
| Key Pad Lock On | be ef 10 05 00 1d 3e 11 11 01 00 24 |
| Key Pad Lock Off | be ef 10 05 00 dd ff 11 11 01 00 25 |
| ECO Mode On | be ef 10 05 00 d9 bf 11 11 01 00 2a |
| ECO Mode Off | be ef 10 05 00 19 7e 11 11 01 00 2b |
| Auto Source On | be ef 10 05 00 db 3f 11 11 01 00 2c |
| Auto Source Off | be ef 10 05 00 1b fe 11 11 01 00 2d |
| Factory Reset | be ef 10 05 00 1a be 11 11 01 00 2e |
| Mute Off | be ef 10 05 00 3c 98 11 11 01 00 5f |
| Unhide | be ef 10 05 00 ed 3f 11 11 01 00 64 |
| Source-VGA Analog 2 | be ef 10 05 00 28 fe 11 11 01 00 69 |

# Comandos de Leitura (Queries)

| Query | Pacote Hexadecimal |
| :--- | :--- |
| System Status | be ef 10 05 00 46 7e 11 11 01 00 ff |
| Lamp Hour | be ef 10 05 00 da 7f 11 11 01 00 2f |
| Firmware Version | be ef 10 05 00 12 3e 11 11 01 00 30 |
| Current Source | be ef 10 05 00 dc bf 11 11 01 00 26 |
| Brightness Read | be ef 10 05 00 10 be 11 11 01 00 36 |
| Contrast Read | be ef 10 05 00 d4 3f 11 11 01 00 38 |
| Get Mute State | be ef 10 05 00 ee ff 11 11 01 00 61 |
| Get Hide State | be ef 10 05 00 2d fe 11 11 01 00 65 |
