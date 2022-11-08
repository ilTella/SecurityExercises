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