# Codigo-Mips-Tarea-
.data
buffer: .space 16777216

.text

loop:
la $s0, 0x10010000
li $v0, 5
syscall
move $t0, $v0
li $v0, 5
syscall
move $t1, $v0
li $v0, 5
syscall
move $t2, $v0
sll $t0, $t0, 16
sll $t1, $t1, 8
add $t0, $t0, $t1
add $t0, $t0, $t2
addi $s2, $s2, 1
sw $t0, 0($s0)
addi $s0, $s0, 4
bne $s2, 1048576, loop
j main


main:
la $s1, buffer
la $s0, 0x10010000
li $v0,  5
syscall
beq $v0, 1, rotate
beq $v0, 2, mirror
syscall
j main




mirror:
addi $s1, $s1, 4092
li $s4, 4096
li $s5, 0
loop1:
lw $t0, 0($s0)
sw $t0, 0($s1)
addi $s0, $s0, 4
subi $s1, $s1, 4
addi $s5, $s5, 4
bne $s5, $s4, loop1
addi $s1, $s1, 8188
addi $s4, $s4, 4096
ble $s4, 16777216, loop1
la $s0, 0x10010000
la $s1, buffer
li $s4 4096
j volver

rotate:
li $s4, 4
li $s5, 0
li $s6 4092
addi $s1, $s1, 4092
loop2:
lw $t0, 0($s0)
sw $t0, 0($s1)
addi $s1, $s1, 4096
addi $s0, $s0, 4
addi $s5, $s5, 4
bne $s6, $s5, loop2
add $s6, $s6, 4096
la $s1, buffer
li $t0, 4092
sub $t0, $t0, $s4
mult $t0, $s4
addi $s4, $s4, 4
mflo $t0
add $s1, $s1, $t0
ble $t0, 16773120, loop2
j volver

volver:
addi $s1, $s1, 4092
li $s4, 4096
loop3:
lw $t0, 0($s0)
sw $t0, 0($s1)
addi $s0, $s0, 4
addi $s1, $s1, 4
bne $s0, $s4, loop3
addi $s4, $s4, 4096
ble $s4, 16777216, loop3
j main
(commit 3)
