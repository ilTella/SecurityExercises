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