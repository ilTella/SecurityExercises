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