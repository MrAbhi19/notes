# RISC-V Pipeline and Base ISA

## Classic Five-Stage RISC Pipeline
A typical RISC processor executes instructions through five stages:
1. **Instruction Fetch (IF)** – Retrieve the instruction from memory.
2. **Instruction Decode (ID)** – Interpret the instruction and read registers.
3. **Execute (EX)** – Perform the operation (ALU computation, address calculation).
4. **Memory Access (MEM)** – Read or write data from/to memory if required.
5. **Write Back (WB)** – Store results back into registers.

---

## Base Integer ISAs
The RISC-V unprivileged ISA defines four base integer instruction sets:
- **RV32I** – 32-bit integer
- **RV32E** – 32-bit embedded (reduced register set)
- **RV64I** – 64-bit integer
- **RV128I** – 128-bit integer

---

## Assembler Directives

### Code and Data Sections
- **`.text`** – Marks program/instruction code section.
- **`.data`** – Defines initialized, modifiable data.
- **`.rodata`** – Defines initialized, read-only data (constants).
- **`.bss`** – Defines uninitialized, modifiable data.
- **`.section <type>`** – Explicitly defines a section type.

### Constants and Strings
- **`.equ`** – Assigns a name to a constant value.
- **`.ascii`** – Stores ASCII string (no null terminator).
- **`.asciz` / `.string`** – Stores ASCII string with a null terminator.

### Data Storage
- **`.byte`** – 8-bit values.
- **`.half`** – 16-bit values.
- **`.word`** – 32-bit values.
- **`.dword`** – 64-bit values.
- **`.zero n`** – Reserves `n` zero-initialized bytes.

### Memory Alignment
- **`.align n`** – Aligns data to `2^n` bytes by inserting padding.

### Symbols and Entry Points
- **`.globl symbol_name`** – Makes a symbol visible to the linker.
- **`_start`** – Required entry point symbol for program execution.

---

## Linker Scripts
While the default linker script is used in the GNU toolchain, custom linker scripts are crucial in embedded systems. They define the memory layout and specify how sections (`.text`, `.data`, `.bss`, etc.) are placed in memory.
