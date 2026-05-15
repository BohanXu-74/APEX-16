# APEX-16 Pipeline

> ⚠️ Early stage — details subject to change.

## Overview

APEX-16 uses a **6-stage in-order pipeline**:

```
┌────────┐   ┌────────┐   ┌──────┐   ┌─────┐   ┌─────┐   ┌───────────┐
│ Fetch  │ → │ Decode │ → │ Reg  │ → │ ALU │ → │ MEM │ → │ Reg Write │
└────────┘   └────────┘   └──────┘   └─────┘   └─────┘   └───────────┘
```

## Stage Descriptions

### 1. Fetch
Retrieve the next instruction from memory using the program counter (PC).

### 2. Decode
Break the instruction into opcode, source registers, destination register, and any immediate values.

### 3. Register Read
Read the values from the source registers specified by the decoded instruction.

### 4. ALU / FPU
Execute the operation:
- Integer/logic ops → ALU
- Floating point ops → FPU

### 5. Memory
For load/store instructions, access RAM here. For non-memory instructions, this stage passes through.

### 6. Register Write
Write the result of the operation back to the destination register.

---

## V1 vs V2

V1 was scrapped because:
- Pipeline stalls were too complex to resolve cleanly
- The design was too rigid and hard to debug
- Too many tightly coupled stages

V2 simplifies the pipeline and makes stages more modular and independent.

---

## Known Challenges (To Be Solved)
- Data hazards (read-after-write)
- Control hazards (branches)
- Stall / forwarding logic

These are active design problems for V2.
