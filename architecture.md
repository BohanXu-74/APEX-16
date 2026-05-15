# APEX-16 Architecture

> ⚠️ Early stage — details subject to change.

## Word Size
- **16-bit** data width throughout

## Pipeline Stages

| Stage | Name | Description |
|---|---|---|
| 1 | Fetch | Fetch instruction from memory |
| 2 | Decode | Decode opcode and operands |
| 3 | Register Read | Read source registers |
| 4 | ALU / FPU | Execute operation |
| 5 | Memory | Read/write RAM if needed |
| 6 | Register Write | Write result back to register |

## Register File

| Register | Role |
|---|---|
| A | Accumulator |
| R1–R? | General purpose (count TBD, ~8 total) |
| ADDR? | RAM addressing registers (count TBD) |

All registers are **16-bit wide**.

## ALU

Supported operations:
- **Logic:** AND, OR, NAND, NOT, XOR
- **Shift:** Shift Left, Shift Right
- **Compare:** Less than, Greater than, Equal

## FPU

Supports:
- Floating point **addition**
- Floating point **subtraction**

Format: TBD (standard format planned)

## ISA

Instruction set not yet finalized. To be documented here once designed.

## Virtual Memory

Under consideration — not yet confirmed for V2.
