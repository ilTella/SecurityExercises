# Assembly exercises
To compile and give solution:
```
gcc -nostdlib -static -o file file.s
objcopy --dump-section .text=RawFile file
cat RawFile | /challenge/level_x
```
Before each source code:
```
.intel_syntax noprefix
.global _start
_start:
```
## ex 1
## ex 2
## ex 3
## ex 4
## ex 5
## ex 6
+ use only these instructions: mov
+ rax = rdi % 256
+ rbx = rsi % 65536
```
mov     al, dil
mov     bx, si
```
## ex 7
+ use only these instructions: mov, shr, shl
+ rax = the 5th least significant byte of rdi
```
shr     rdi, 32 # 4*8
shl     rdi, 56 # 7*8
shr     rdi, 56
mov     al, dil
```
## ex 8
+ do NOT use these instructions: mov, xchg
+ rax = rdi AND rsi
```
and     rdi, rsi
xor     rax, rax
or      rax, rdi
```
## ex 9
+ use only the instructions: and, or, xor
+ if rdi is even, then rax = 1, rax = 0 otherwise
```
xor     rax, rax 
or      rax, 1         # rax = 1
and     rdi, 1         # rdi = 0 if even, 1 if odd
xor     rax, rdi       # if rdi == 1, rax = 0 and vice versa
```
## ex 10
+ move the value stored at 0x404000 into rax
+ increment the value stored at the address 0x404000 by 0x1337
```
mov     rax, [0x404000]
mov     rdi, rax
add     rdi, 0x1337
mov     [0x404000], rdi
```
## ex 11
+ rax = byte at 0x404000
+ rbx = word at 0x404000
+ rcx = double word at 0x404000
+ rdx = quad word at 0x404000
```
mov     al, [0x404000]
mov     bx, [0x404000]
mov     ecx, [0x404000]
mov     rdx, [0x404000]
```
## ex 12
+ [rdi] = 0xdeadbeef00001337
+ [rsi] = 0xc0ffee0000
```
mov     rax, 0xdeadbeef00001337
mov     rbx, 0xc0ffee0000
mov     [rdi], rax
mov     [rsi], rbx
```
## ex 13
+ load two consecutive quad words from the address stored in rdi
+ calculate the sum of the previous steps quad words.
+ [rsi] = sum
```
mov     rax, [rdi]
mov     rbx, [rdi + 8]
add     rax, rbx
mov     [rsi], rax
```
## ex 14
+ subtract rdi from the top value on the stack
```
pop     rax
sub     rax, rdi
push    rax
```
## ex 15
+ use only the instructions: push, pop
+ swap values in rdi and rsi
```
push    rdi
push    rsi
pop     rdi
pop     rsi
```
## ex 16
+ do NOT use these instructions: pop
+ calculate the average of 4 consecutive quad words stored on the stack
+ store the average on the top of the stack
```
mov     rax, [rsp]
mov     rbx, [rsp + 8]
mov     rsi, [rsp + 16]
mov     rdi, [rsp + 24]

add     rax, rbx
add     rax, rsi
add     rax, rdi

shr     rax, 2          # divide rax by 4

mov     [rsp - 8], rax
```
## ex 17
+ create a two jump trampoline:
1. make the first instruction in your code a jmp
2. make that jmp a relative jump to 0x51 bytes from its current position
3. at 0x51 write the following code:
4. place the top value on the stack into register rdi
5. jmp to the absolute address 0x403000
```
jmp     .code
81 x nop
.code:
pop     rdi
mov     rax, 0x403000
jmp     rax
```
## ex 18
+ use at least once the following instructions: jmp (any variant), cmp
+ implement the following:  
if [rdi] is 0x7f454c46:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rax = [rdi + 4] + [rdi + 8] + [rdi + 12]  
else if [rdi] is 0x00005A4D:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rax = [rdi + 4] - [rdi + 8] - [rdi + 12]  
else:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rax = [rdi + 4] * [rdi + 8] * [rdi + 12]  

```
mov     r8d, [rdi]
cmp     r8d, 0x7f454c46
jne     elseif
mov     eax, [rdi + 4]
add     eax, [rdi + 8]
add     eax, [rdi + 12]
jmp     done

elseif:
cmp     r8d, 0x00005A4D
jne     else
mov     eax, [rdi + 4]
sub     eax, [rdi + 8]
sub     eax, [rdi + 12]
jmp     done

else:
mov     eax, [rdi + 4]
mov     r9d, [rdi + 8]
mul     r9d
mov     r9d, [rdi + 12]
mul     r9d

done:
```

## ex 19
+ assume rdi will NOT be negative
+ use no more than 1 cmp instruction
+ use no more than 3 jumps (of any variant)
+ we will provide you with the number to 'switch' on in rdi.
+ we will provide you with a jump table base address in rsi.
```
if rdi is 0:
    jmp 0x403008
else if rdi is 1:
    jmp 0x403114
else if rdi is 2:
    jmp 0x4031cf
else if rdi is 3:
    jmp 0x403294
else:
    jmp 0x403349
```
```
cmp     rdi, 4
jge     else
jmp     [rsi + rdi * 8]

else:
jmp     [rsi + 0x20]
```

## ex 20
Please compute the average of n consecutive quad words, where:  
+ rdi = memory address of the 1st quad word  
+ rsi = n (amount to loop for)  
+ rax = average computed  
```
xor     rax, rax
xor     r8, r8

loop:
cmp     rsi, r8
je      done

add     rax, [rdi + r8 * 8]
inc     r8
jmp     loop

done:
div     rsi
```

## ex 21
```
average = 0
i = 0
while x[i] < 0xff:
    average += x[i]
    i += 1
average /= i
```
Using the above knowledge, please perform the following:
Count the consecutive non-zero bytes in a contiguous region of memory, where:
rdi = memory address of the 1st byte
rax = number of consecutive non-zero bytes
Additionally, if rdi = 0, then set rax = 0
```
cmp     rdi, 0
jne     function
xor     rax, rax
jmp     done

function:
xor     r8, r8
xor     rax, rax
while:
mov     r9, [rdi + r8]
cmp     r9, 0
je      done
inc     r8
inc     rax
jmp     while

done:
```

## ex 22
Please implement the following logic: 
``` 
str_lower(src_addr):
    rax = 0
    if src_addr != 0:
        while [src_addr] != 0x0:
            if [src_addr] <= 90:
                [src_addr] = foo([src_addr])
                rax += 1
            src_addr += 1
```
foo is provided at 0x403000. foo takes a single argument as a value  
```
str_lower:
xor     rax, rax                            # rax = 0
cmp     rdi, 0                              # if src_addr != 0
je      done
    while:
    mov     r8, [rdi]
    cmp     r8, 0
    je      done                            # while [src_addr] != 0
        cmp     r8, 90
        jg     notif                        # if [src_addr] <= 90
            push    rax
            push    rdi
            mov     rax, 0x403000
            mov     rdi, [rdi]
            call    rax
            pop     rdi
            mov     [rdi], rax              # [src_addr] = foo([src_addr])
            pop     rax
            inc     rax                     # rax += 1
        notif:
        inc     rdi                         # src_addr += 1
        jmp     while
done:
xor     rax, rax 
ret
```  
???

## ex 23
???