# Random Access Memory
The Ranom Access Memory (RAM) is where the [[Emulator]] stores data. The RAM provides 65535 bits of storage.

RAM can be accessed at any time by the [[Central Processing Unit|CPU]]'s [[Interpreter]]. To modify RAM, please use the [[Interpreter#Instructions]] `0x04`.

## Allocated RAM
| Address | Size | Usage |
| --- | --- | --- |
| `0x0000` | `0x00ff` | Used to store cursor positions ([[Interpreter#Checkpoints]]). |