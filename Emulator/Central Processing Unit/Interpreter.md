# Interpreter
Reads and executes [[Interpreter#Instructions]].

The interpreter reads the [[Program Memory]] and executes one by one every [[Interpreter#Instructions|instruction]] written in.

## Summary
1. [[Interpreter#Instructions]]
1. [[Interpreter#Checkpoints]]

## Instructions
Format:
- First byte indicates the operator
- Following bytes are the operands

### Instructions definitions

| Operator | Operands | Description |
| --- | --- | --- |
| `0x01` | `checkpointID` | Set a [[Checkpoints\|checkpoint]] in the program. |
| `0x02` | `checkpointID` | Go to a specific [[Checkpoints\|checkpoint]]. |
| `0x03` |  | Go back to the last position. |
| `0x04` | `destinationType`, `destination`, `valueType`, `value` | Set the value of a variable to another.
| `0x05` | `valueType`, `value` | Add a value to the [[Stack]]. |
| `0x06` | `destinationType`, `destination` | Remove the last value from the [[Stack]], and stores it at the specified destination. |
| `0x07` | `destination`, `value`, [[Arithmetic Logic Unit#Operations types\|Operation]] | Sends an [[Arithmetic Logic Unit#Instructions\|instruction]] the [[Arithmetic Logic Unit]].

### Operands definitions

| Operand | Number of bits | Accepted values | Description |
| --- | --- | --- | --- |
| `checkpointID` | 16 | Any | ID of checkpoint, used to navigate inside programs |
| `destination` | 8 \| 16 | [[Registers\|Register]] ID <br/> [[Random Access Memory\|RAM]] address | Destination. Widly used to change variables. |
| `destinationType` | 8 \| 8 | [[Registers\|Register]] : `0x0` <br/> [[Random Access Memory\|RAM]] address : `0x1` | Specifies whether the chosen destination is a register or in the RAM. |
| `value` | 8 \| 16 \| 16 | [[Registers\|Register]] ID <br/> [[Random Access Memory\|RAM]] address <br/> Any | Represents a value, in a register, in the RAM or raw. |
| `valueType` | 8 \| 8 \| 8 | [[Registers\|Register]] : `0x0` <br/> [[Random Access Memory\|RAM]] address : `0x1` <br/> Any : `0x2` | Specifies whether the chosen value is in a register, in the RAM or raw. |


# Checkpoints
Used by the [[Interpreter]] to navigate back through programs.

When an [[Interpreter#Instructions|Instruction]] `0x2` is executed by the [[Interpreter]], 4 of the `0xff` [[Random Access Memory]] allocated bytes is set to the previous program cursor location. These bytes are set back to 0 when the [[Interpreter#Instructions|Instruction]] `0x3` is executed.