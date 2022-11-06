# Assembly exercises
```
gcc -nostdlib -static -o file file.s
objcopy --dump-section .text=RawFile file
cat RawFile | /challenge/level_x
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