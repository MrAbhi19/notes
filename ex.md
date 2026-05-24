# Multiplication
```asm
addi x1, x0, 10
addi x2, x0, 4

addi x3, x0, 0

mul:
add x3, x3, x1
addi x2, x2, -1

bne x2, x0, mul
```

# Sum of first n-natural numbers
```asm
addi x1, x0, 50

addi x2, x0, 0

sum:
add x2, x2, x1
addi x1, x1, -1

bne x1, x0, sum
```
OR
```asm
addi x1, x0, 50

addi x2, x0, 0
addi x3, x0, 1

loop:
bgt x3, x1, done

add x2, x2, x3
addi x3, x3, 1

j loop

done:
```

# Number of Even and Odd
```asm
addi x1, x0, 10

addi x2, x0, 0
addi x3, x0, 0

srai x2, x1, 1   # no. of Even numbers
sub x3, x1, x2   # no. of Odd numbers
```

# Square of number N
```asm
addi x1, x0, 10

addi x2, x0, 0
add x3, x0, x1

sq:
add x2, x2, x1
addi x3, x3, -1

bne x3, x0, sq
```

# Finding bigger number
```asm
addi x1, x0, 16
addi x2, x0, 15

addi x3, x0, 0

blt x1, x2, one

add x3, x0, x1
jal x0, done

one:
add x3, x0, x2
done:
```
