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

# Square if number with functions 
```asm
.text
.globl main

main:
addi a0 x0 1
jal ra square

done:
beq x0 x0 done

square:
addi t0 a0 0
addi t1 x0 0 
addi t2 a0 0

loop:
add t1 t1 t0
addi t2 t2 -1 

bne t2 x0 loop

add a0 t1 x0

jalr x0 0(ra)
```

# Sum of squares of first N natural numbers
```asm
.text
.globl main

main:
    addi a0 x0 4
    jal sum_sq

done:
    beq x0 x0 done


sum_sq:
    addi sp sp -16
    sw ra 12(sp)
    sw s0 8(sp)
    sw s1 4(sp)
    sw s2 0(sp)
    
    add s0 a0 x0  # number n 
    addi s1 x0 0  # counter
    add s2 x0 x0  # running sum
    
sm_loop:
    addi s1 s1 1
    add a0 s1 x0
    jal sq
    add s2 s2 a0
    
    bne s1 s0 sm_loop
    
    add a0 s2 x0
    
    lw ra 12(sp)
    lw s0 8(sp)
    lw s1 4(sp)
    lw s2 0(sp)
    addi sp sp 16
    
    jalr x0 ra 0

    
sq:
    add t0 a0 x0
    add t1 a0 x0
    add t2 x0 x0
    
sq_loop:
    add t2 t2 t1
    addi t0 t0 -1
    
    bne t0 x0 sq_loop
    
    add a0 t2 x0
    
    jalr x0 ra 0
```

#Sum of numbers stored in memory 
```asm
.data
array: .word 10, 20, 15, 35, 25, 7, 18
N: .word 7

.text
.globl main

main:
la t0 array

la t1 N
lw t1 0(t1)

addi t2 x0 0
addi t3 x0 0

loop:
beq t3 t1 done

lw t4 0(t0)

add t2 t2 t4
addi t0 t0 4

addi t3 t3 1

beq x0 x0 loop

done:
add a0 t2 x0
```
