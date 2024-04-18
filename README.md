.org 0x10000000

li $t0, 0xf0100000  # Address where switches are mapped
li $t1, 0xf0200000  # Address where LEDs are mapped

main_loop:
    
    lw $t3, 0($t0)     # Load the current switch value into $t3

    li $t4, 0x01        # Hex value for switch 0
    beq $t3, $t4, switch_0

    li $t4, 0x02        # Hex value for switch 1
    beq $t3, $t4, switch_1

    li $t4, 0x04        # Hex value for switch 2
    beq $t3, $t4, switch_2

    li $t2, 0x00       # Default to all LEDs off if no condition met
    sw $t2, 0($t1)
    j main_loop        # Repeat the loop indefinitely

switch_0:

    li $t2, 0x0F       # Turn on LEDs 0, 1, 2, and 3
    sw $t2, 0($t1)
    nop                # Short delay for scrolling
    li $t2, 0x00       # Turn off LEDs
    sw $t2, 0($t1)
    j main_loop

switch_1:

    li $t2, 0xF0       # Turn on LEDs 4, 5, 6, and 7
    sw $t2, 0($t1)
    nop                # Short delay for scrolling
    li $t2, 0x00       # Turn off LEDs
    sw $t2, 0($t1)
    j main_loop

switch_2:

    li $t2, 0x02       # LED 1 on
    sw $t2, 0($t1)
    nop                # Short delay for scrolling

    li $t2, 0x08       # LED 3 on
    sw $t2, 0($t1)
    nop                # Short delay for scrolling

    li $t2, 0x20       # LED 5 on
    sw $t2, 0($t1)
    nop                # Short delay for scrolling

    li $t2, 0x80       # LED 7 on
    sw $t2, 0($t1)
    nop                # Short delay for scrolling

    li $t2, 0x00       # Turn off LEDs
    sw $t2, 0($t1)
    j main_loop
