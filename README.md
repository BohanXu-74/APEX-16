# APEX-16
### Advanced Pipelined EXecution — 16-bit CPU

> ⚠️ **This project is in early development. Specifications are subject to change.**

APEX-16 is a custom-designed 16-bit pipelined CPU with a floating point unit (FPU), built entirely in [Digital](https://github.com/hneemann/Digital) — a logic circuit simulator by hneemann. The project is inspired by Intel i386–Pentium architecture, IEEE floating point, and classic pipelining techniques.

---

## Features (Planned / In Progress)

| Feature | Status |
|---|---|
| 16-bit architecture | 🔄 In Progress |
| 6-stage pipeline | 🔄 In Progress |
| ALU (logic + arithmetic) |  🔄 In Progress  |
| FPU (floating point add/sub) |  📋 Planned |
| General purpose registers (~8) | 🔄 In Progress |
| Accumulator register (Reg A) | 🔄 In Progress |
| RAM addressing registers | 📋 Planned |
| ISA (Instruction Set) | 📋 Planned |
| Virtual memory | ❓ Under Consideration |

---

## Architecture

### Pipeline

APEX-16 uses a **6-stage in-order pipeline**:

```
┌────────┐   ┌────────┐   ┌──────┐   ┌─────┐   ┌─────┐   ┌───────────┐
│ Fetch  │ → │ Decode │ → │ Reg  │ → │ ALU │ → │ MEM │ → │ Reg Write │
└────────┘   └────────┘   └──────┘   └─────┘   └─────┘   └───────────┘
```

| Stage | Name | Description |
|---|---|---|
| 1 | Fetch | Retrieve the next instruction from memory via the program counter |
| 2 | Decode | Break the instruction into opcode, operands, and register targets |
| 3 | Register Read | Read source register values |
| 4 | ALU / FPU | Execute the operation — integer ops go to ALU, float ops go to FPU |
| 5 | Memory | Load/store RAM access; passes through for non-memory instructions |
| 6 | Register Write | Write the result back to the destination register |

#### Known Challenges (Active Design Problems)
- Data hazards (read-after-write)
- Control hazards (branches)
- Stall and forwarding logic

---

### Registers

All registers are **16-bit wide**.

| Register | Role |
|---|---|
| A | Accumulator |
| R1–R? | General purpose (~8 total, count TBD) |
| ADDR? | RAM addressing registers (count TBD) |

---

### ALU — Arithmetic Logic Unit

| Category | Operations |
|---|---|
| Logic | AND, OR, NAND, NOT, XOR |
| Shift | Shift Left, Shift Right |
| Compare | Less than, Greater than, Equal |

---

### FPU — Floating Point Unit

| Operation | Status |
|---|---|
| Addition | 🔄 In Progress |
| Subtraction | 🔄 In Progress |

Float format: TBD — standard format planned.

---

### CMU — Complex Math Unit

> ❓ This unit's role is still under consideration and may change or be removed.

---

### ISA — Instruction Set Architecture

Not yet finalized. Will be documented here once designed.

---

## Repository Structure

```
APEX-16/
├── README.md
├── src/
│   ├── ALU/                  # ALU circuit files (.dig)
│   ├── FPU/                  # FPU circuit files (.dig)
│   ├── CMU/                  # CMU circuit files (.dig)
│   ├── CPU/                  # MAIN CPU with all of the connecting circuts including Registers
├── diagrams/                 # PNG exports of circuit diagrams
└── tests/                    # Test programs / simulations (Not yet made)
```

---

## Project Log

### V2 — Current
Redesigned from scratch. V1 was scrapped due to:
- Pipeline stall complexity that was unsolvable in the original design
- Overly rigid structure with low flexibility
- Too many tightly coupled layers making debugging extremely difficult

V2 focuses on simplicity, shorter pipeline stages, and cleaner modularity.

### V1 — Scrapped
Original design. Files preserved for reference.

---

## Tools Used

- **[Digital](https://github.com/hneemann/Digital)** — logic circuit simulator (`.dig` files)

---

## Inspiration & References

- *Intel CPU Architecture: i386–Pentium* (book)
- [MIT OpenCourseWare — Pipelining lecture](https://ocw.mit.edu)
- [NAND Game](https://nandgame.com) — floating point logic via logic gates

---

## Author

**Bohan Xu**
- Hackaday: [hackaday.io/project/205126](https://hackaday.io/project/205126-16-bit-pipelined-cpu-with-fpu)
- Also building: [8-bit CPU from Scratch](https://hackaday.io/project/204995-8-bit-cpu-from-scratch)

---

## Status

🚧 Active development — Early Stage
