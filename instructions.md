## R-type Instructions

```asm
add x1, x0, x2      # x1 = x0 + x2
sub x3, x2, x4      # x3 = x2 - x4
and x5, x2, x1      # x5 = x2 & x1
or  x6, x2, x1      # x6 = x2 | x1
xor x7, x2, x1      # x7 = x2 ^ x1

sll a1, x2, x1      # a1 = x2 << x1   (logical left shift)
srl a2, x2, x1      # a2 = x2 >> x1   (logical right shift)
sra a3, x2, x1      # a3 = x2 >> x1   (arithmetic right shift)

slt  a4, x2, x1     # a4 = 1 if x2 < x1 (signed)
sltu a5, x2, x1     # a5 = 1 if x2 < x1 (unsigned)
```

---

## S-type Instructions

```asm
sb x2, 1(x1)        # Store byte (8-bit) at address (x1 + 1)
sh x2, 3(x1)        # Store halfword (16-bit) at address (x1 + 3)
sw x2, 0(x1)        # Store word (32-bit) at address (x1 + 0)
```

## I-type Instructions (Load)

```asm
lb  x1, 1(x2)       # Load signed byte from address (x2 + 1)
lbu x3, 1(x2)       # Load unsigned byte from address (x2 + 1)

lh  x4, 3(x2)       # Load signed halfword from address (x2 + 3)
lhu x5, 3(x2)       # Load unsigned halfword from address (x2 + 3)

lw  x6, 0(x2)       # Load word from address (x2 + 0)
```

## Immediate Arithmetic Instructions

```asm
addi x1, x0, 13    # x1 = x0 + 13
andi x2, x1, 9     # x2 = x1 & 9
ori x2, x1, 16     # x2 = x1 | 16
xori x2, x1, 3     # x2 = x1 ^ 3
slti x2, x1, 3     # x2 = 1 if x1 < 3  (signed)  
sltiu x2, x1, 2    # x2 = 1 if x1 < 2  (unsigned)
slli x2, x1, 1     # x2 = x1 << 1      (logical left shift)
srli x2, x1, 2     # x2 = x1 >> 2      (logical right shift)
srai x2, x1, 2     # x2 = x1 >> 2      (arithmetic right shift)
```

## jump and link register 
```asm
jalr x1, 0(x2)     # x1 = PC + 4,  PC = PC + (x2 + 0)
```

## U-type Instructions 
```asm
lui x1, 20      # x1 = 20 << 12
auipc x2, 20    # x2 = PC + (20 << 12)
```

## J-type instruction
```asm
jal x1, 20      # x1 = PC + 4,  PC = PC + 20
```

## B-tyoe instructions 
```asm
beg x1, x2, 20   # if (x1 == x2): PC = PC + 20
                   else: PC = PC + 4
bne x1, x2, 20   # if (x1 =! x2): PC = PC + 20
                   else: PC = PC + 4
blt x1, x2, 20   # if (x1 < x2): PC = PC + 20
                   else: PC = PC + 4 (signed)
bge x1, x2, 20   # if (x1 >= c2): PC = PC + 20
                   else: PC = PC + 4 (signed)
bltu x1, x2, 20  # if (x1 < x2): PC = PC + 20
                   else: PC = PC + 4 (unsigned)
bgeu x1, x2, 20  # if (x1 >= c2): PC = PC + 20
                   else: PC = PC + 4 (unsigned)
```









               else: PC = PC + 4 (signed)
