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
+ only use these instructions: mov
+ rax = rdi % 256
+ rbx = rsi % 65536
```
mov     al, dil
mov     bx, si
```
## ex 7
+ only use these instructions: mov, shr, shl
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