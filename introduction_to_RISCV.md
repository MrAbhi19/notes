# RISC-V Architecture — Revision Notes

---

## 1. Base Integer ISA — RV32I

The **RV32I** is the foundation of RISC-V. It has only **40 instructions** — just enough to get things working with 32-bit integers. The 64-bit variant is **RV64I**.

### What RV32I Can Do
- Addition & Subtraction
- Bitwise logical operations (AND, OR, XOR, etc.)
- Load & Store (memory access)
- Jumps & Branches (control flow)

### Registers
- **32 general-purpose registers** (x0–x31), each 32 bits wide
- **1 Program Counter (PC)**
- **x0 is special** — it always reads as zero (hardwired), a common RISC design pattern

---

## 2. ABI Register Names (Application Binary Interface)

| Register | ABI Name | Description                       | Saved By |
|----------|----------|-----------------------------------|----------|
| x0       | zero     | Hard-wired zero                   | —        |
| x1       | ra       | Return address                    | Caller   |
| x2       | sp       | Stack pointer                     | Callee   |
| x3       | gp       | Global pointer                    | —        |
| x4       | tp       | Thread pointer                    | —        |
| x5       | t0       | Temporary / alt link register     | Caller   |
| x6–x7    | t1–t2    | Temporaries                       | Caller   |
| x8       | s0/fp    | Saved register / frame pointer    | Callee   |
| x9       | s1       | Saved register                    | Callee   |
| x10–x11  | a0–a1    | Function args / return values     | Caller   |
| x12–x17  | a2–a7    | Function arguments                | Caller   |
| x18–x27  | s2–s11   | Saved registers                   | Callee   |
| x28–x31  | t3–t6    | Temporaries                       | Caller   |

> **Caller** = the function that calls another function  
> **Callee** = the function that gets called

---

## 3. Control and Status Registers (CSRs)

CSRs are a **separate bank of registers** with a 12-bit address space → up to **4096 CSRs**.

### Key CSRs to Know

| CSR       | Full Name                        | Purpose |
|-----------|----------------------------------|---------|
| `mstatus` | Machine Status Register          | Controls privilege level, interrupt enable/disable, processor behavior flags |
| `mepc`    | Machine Exception Program Counter| Stores PC of the instruction that caused an exception — used to resume after handling |
| `mtvec`   | Machine Trap-Vector Base Address | Points to the trap handler — where CPU jumps on exception |
| `mcause`  | Machine Cause Register           | Tells you *why* an exception/interrupt happened (e.g. page fault, software interrupt) |
| `misa`    | Machine ISA Register             | Lists supported ISA extensions and encodes bit-width (RV32/64/128) |

---

## 4. Privilege Modes

RISC-V defines four privilege levels, from most to least privileged:

| Mode   | Name             | Use Case |
|--------|------------------|----------|
| M-mode | Machine mode     | Bare metal, firmware, most privileged |
| H-mode | Hypervisor mode  | Virtualization |
| S-mode | Supervisor mode  | OS kernels |
| U-mode | User mode        | Regular applications |

> Extensions that don't require M-mode are described in the **unprivileged specification**.

---

## 5. Instruction Formats

RISC-V has 6 instruction encoding formats:

| Format | Used For |
|--------|----------|
| **R-type** | Register-to-register operations |
| **I-type** | Immediate values, loads |
| **S-type** | Stores |
| **B-type** | Branches |
| **U-type** | Upper immediate |
| **J-type** | Jumps |

---

## 6. ISA Extensions

Each extension is developed by a dedicated **task group**. Extensions are added to the base ISA as letters.

### Core Extensions

| Extension | Name / Purpose | Notes |
|-----------|---------------|-------|
| **M** | Integer Multiply & Divide | 8 instructions (RV64M adds 5 more) |
| **F** | Single-Precision Float (32-bit) | Adds f0–f31 registers; follows IEEE 754 |
| **D** | Double-Precision Float (64-bit) | Extends f0–f31 to 64-bit; follows IEEE 754 |
| **A** | Atomic Memory Operations | For thread-safe memory access |
| **Q** | Quad-Precision Float (128-bit) | 128-bit floating point registers |
| **B** | Bit Manipulation | Speeds up common math tasks |
| **S** | Supervisor Operations | OS-level features |
| **H** | Hypervisor Operations | Virtualization support |
| **L** | Decimal Floating-Point | *Still under discussion* |
| **P** | Packed-SIMD Instructions | *Still under discussion* |
| **V** | Vector Operations | Key for graphics/parallel computation |
| **Zicsr** | CSR Manipulation | Read/write CSR registers |
| **Zifencei** | Instruction Memory Sync | Ensures instruction cache coherence |

> ✅ Most extensions are **ratified** (finalized).  
> ⏳ **L** and **P** extensions are still open/under discussion.

### Notable Task Groups

- **Crypto** — moves cryptographic algorithms into hardware for speed & reliability
- **B Extension** — bit manipulation for faster math
- **Vector (V)** — vector instructions for graphics & parallel workloads

---

## 7. Floating Point — F vs D at a Glance

| Feature | F Extension | D Extension |
|---------|------------|------------|
| Precision | Single (32-bit) | Double (64-bit) |
| Registers | f0–f31 (32-bit wide) | f0–f31 (64-bit wide) |
| Standard | IEEE 754 | IEEE 754 |
| Use Case | General embedded | Scientific & engineering |
| Handles NaN/Inf? | ✅ | ✅ |

> Many embedded systems skip F and D entirely — they're not part of the base ISA.

---
