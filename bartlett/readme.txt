The general form of memory address references:
    ADDRESS_OR_OFFSET(%BASE_OR_OFFSET,%INDEX,MULTIPLIER)
    FINAL ADDRESS = ADDRESS_OR_OFFSET + %BASE_OR_OFFSET + MULTIPLIER * %INDEX

direct addressing mode
    movl ADDRESS, %eax

indexed addressing mode
    movl string_start(,%ecx,1), %eax

indirect addressing mode
    movl (%eax), %ebx
# %eax held an address

base pointer addressing mode
    movl 4(%eax), %ebx

immediate mode
    movl $12, %eax

register addressing mode

================================================

Programming can either be viewed as breaking a large program down into smaller pieces until you get to the primitive functions, or incrementally building functions on top of primitives until you get the large picture in focus.

Every time we push something onto the stack with pushl , %esp gets subtracted by 4 so that it points to the new top of the stack (remember, each word is four bytes long, and the stack grows downward).
If we want to remove something from the stack, we simply use the popl instruction, which adds 4 to %esp and puts the previous top value in whatever register you specified.

movl (%esp), %eax
#   If we simply want to access the value on the top of the stack without removing it, we can simply use the %esp register in indirect addressing mode.
#   Putting %esp in parenthesis causes the computer to go to indirect addressing mode, and therefore we get the value pointed to by %esp .

movl %esp, %eax
#   %eax would just hold the pointer to the top of the stack rather than the value at the top.

subl $8, %esp
# This subtracts 8 from %esp (remember, a word is four bytes long).

================================================

"AMD64 architecture programmer's manual vol. 3: general-purpose and system instructions"

CALL(near)     -     near procedure call
pushes the offset of the next instruction onto the stack and branches to the target address, which contains the first instruction of the called procedure.

CALL(far)     -     far procedure call
pushes procedure linking information onto the stack and branches to the target address, which contains the first instruction of the called procedure.

RET(near)     -    near return from called procedure
returns from a procedure previously entered by a CALL near instruction. This form of the RET instruction returns to a calling procedure with the current code segment.

RET(far)     -    near return from called procedure
returns from a procedure previously entered by a CALL far instruction. This form of the RET instruction returns to a calling procedure in a different segment than the current code segment.

PUSH    -     push onto stack
decrements the stack pointer and then copies the specified immediate value or the value in the specified register or memory location to the top of the stack.

POP     -     pop stack
copies the value pointed to by the stack pointer(SS:rSP) to the specified register or memory location and then increments the rSP by 2 for a 16-bit pop, 4 for a 32-bit pop, or 8 for a 64-bit pop.

================================================
