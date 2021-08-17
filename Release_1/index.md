# Release Part 1

## crack_nasm
We using file cmd to check kind of file.
```
                                                                                                                   
┌──(kali㉿kali)-[~/Rev/Release_1/crack_nasm]
└─$ file CrackMe_ASM 
CrackMe_ASM: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), statically linked, not stripped

```
ELF 32bits in excec in Linux 32bits so we can using pwndbg to analysis. 
```
Dump of assembler code for function _start:
   0x08048080 <+0>:     mov    eax,0x4
   0x08048085 <+5>:     mov    ebx,0x1
   0x0804808a <+10>:    mov    ecx,0x8049170
   0x0804808f <+15>:    mov    edx,0x7
   0x08048094 <+20>:    int    0x80
   0x08048096 <+22>:    mov    eax,0x3
   0x0804809b <+27>:    mov    ebx,0x0
   0x080480a0 <+32>:    mov    ecx,0x80491a8
   0x080480a5 <+37>:    mov    edx,0xb
   0x080480aa <+42>:    int    0x80
   0x080480ac <+44>:    mov    eax,0x80491b3
   0x080480b1 <+49>:    mov    BYTE PTR [eax],0x53
   0x080480b4 <+52>:    add    eax,0x1
   0x080480b7 <+55>:    mov    BYTE PTR [eax],0x33
   0x080480ba <+58>:    add    eax,0x1
   0x080480bd <+61>:    mov    BYTE PTR [eax],0x43
   0x080480c0 <+64>:    add    eax,0x1
   0x080480c3 <+67>:    mov    BYTE PTR [eax],0x72
   0x080480c6 <+70>:    add    eax,0x1
   0x080480c9 <+73>:    mov    BYTE PTR [eax],0x45
   0x080480cc <+76>:    add    eax,0x1
   0x080480cf <+79>:    mov    BYTE PTR [eax],0x2b
   0x080480d2 <+82>:    add    eax,0x1
   0x080480d5 <+85>:    mov    BYTE PTR [eax],0x46
   0x080480d8 <+88>:    add    eax,0x1
   0x080480db <+91>:    mov    BYTE PTR [eax],0x6c
   0x080480de <+94>:    add    eax,0x1
   0x080480e1 <+97>:    mov    BYTE PTR [eax],0x34
   0x080480e4 <+100>:   add    eax,0x1
   0x080480e7 <+103>:   mov    BYTE PTR [eax],0x47
   0x080480ea <+106>:   add    eax,0x1
   0x080480ed <+109>:   mov    BYTE PTR [eax],0x21
   0x080480f0 <+112>:   xor    ebx,ebx
   0x080480f2 <+114>:   xor    ecx,ecx
   0x080480f4 <+116>:   mov    ecx,DWORD PTR ds:0x80491b3
   0x080480fa <+122>:   mov    ebx,DWORD PTR ds:0x80491a8
   0x08048100 <+128>:   cmp    ecx,ebx
   0x08048102 <+130>:   jne    0x8048112 <failure>
   0x08048104 <+132>:   jmp    0x8048132 <success>
   0x08048106 <+134>:   call   0x804814f <ClearTerminal>
   0x0804810b <+139>:   mov    eax,0x1
   0x08048110 <+144>:   int    0x80
```
Flow is get input to 0x80491a8 and cmp with string in 0x80491b3.
So we have string: "S3CrE+Fl4G!: from line 26 to 46.

Sovle

## Es crack

Check is first. 
```
┌──(kali㉿kali)-[~/Rev/Release_1/Es crack]
└─$ file run.exe    
run.exe: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), statically linked, with debug_info, not stripped

```
It is a joke. file tail is exe but is a Linux file. So we using pwndbg to analysis.
```
   0x08049000 <+0>:     pop    ebx
   0x08049001 <+1>:     pop    ebx
   0x08049002 <+2>:     pop    ebx
   0x08049003 <+3>:     mov    eax,ds:0x804a000
   0x08049008 <+8>:     cmp    eax,DWORD PTR [ebx]
   0x0804900a <+10>:    je     0x804900e <_start.goodjob>
   0x0804900c <+12>:    jmp    0x8049026 <_start.wrong>
```
It is so clearly and simple. Flow is get input in ebx so cmp eax (0x804a000) . So we check in 0x804a000 and we see : 
```
pwndbg> x/s 0x804a000
0x804a000 <password>:   "P455w0rdYou Got This!\nWrong!\n"<error: Cannot access memory at address 0x804a01d>
```
We have the password and solve

## hello

Using file to check.
```
┌──(kali㉿kali)-[~/Rev/Release_1/hello]
└─$ file hello  
hello: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), statically linked, not stripped

```
So diffrent a little bit, this program is 64bits and nothing change. we still using pwndbg to analysis it.
```
0x0000000000401000 <+0>:     mov    eax,0x1
   0x0000000000401005 <+5>:     mov    edi,0x1
   0x000000000040100a <+10>:    movabs rsi,0x402000
   0x0000000000401014 <+20>:    mov    edx,0x19
   0x0000000000401019 <+25>:    syscall 
   0x000000000040101b <+27>:    mov    eax,0x0
   0x0000000000401020 <+32>:    mov    edi,0x0
   0x0000000000401025 <+37>:    movabs rsi,0x402074
   0x000000000040102f <+47>:    mov    edx,0x20
   0x0000000000401034 <+52>:    syscall 
   0x0000000000401036 <+54>:    cmp    rax,0x0
   0x000000000040103a <+58>:    jl     0x401114 <_start.error>
   0x0000000000401040 <+64>:    mov    r14,rax
   0x0000000000401043 <+67>:    add    r14,0x6
   0x0000000000401047 <+71>:    mov    rax,QWORD PTR ds:0x402019
   0x000000000040104f <+79>:    mov    QWORD PTR ds:0x402094,rax
   0x0000000000401057 <+87>:    mov    rax,QWORD PTR ds:0x402074
   0x000000000040105f <+95>:    mov    QWORD PTR ds:0x40209a,rax
   0x0000000000401067 <+103>:   mov    eax,0x1
   0x000000000040106c <+108>:   mov    edi,0x1
   0x0000000000401071 <+113>:   movabs rsi,0x402094
   0x000000000040107b <+123>:   mov    rdx,r14
   0x000000000040107e <+126>:   syscall 
   0x0000000000401080 <+128>:   mov    eax,0x1
   0x0000000000401085 <+133>:   mov    edi,0x1
   0x000000000040108a <+138>:   movabs rsi,0x402020
   0x0000000000401094 <+148>:   mov    edx,0x16
   0x0000000000401099 <+153>:   syscall 
   0x000000000040109b <+155>:   mov    eax,0x0
   0x00000000004010a0 <+160>:   mov    edi,0x0
   0x00000000004010a5 <+165>:   movabs rsi,0x402074
   0x00000000004010af <+175>:   mov    edx,0x20
   0x00000000004010b4 <+180>:   syscall 
   0x00000000004010b6 <+182>:   mov    r15,rax
   0x00000000004010b9 <+185>:   dec    r15
   
```
Part of piece :<<<



## Lucky

Check file we can see it : 
```
┌──(kali㉿kali)-[~/Rev/Release_1/Lucky]
└─$ file lucky_nb 
lucky_nb: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), statically linked, stripped

```
Becuz it stripped so we can't using gdb to analysis. we using IDA Pro 32bit.
```

.text:0804903A                 mov     eax, 4
.text:0804903F                 mov     ebx, 1          ; fd
.text:08049044                 mov     ecx, offset unk_804A000 ; addr
.text:08049049                 mov     edx, 0Fh        ; len
.text:0804904E                 int     80h             ; LINUX - sys_write
.text:08049050                 mov     eax, 3
.text:08049055                 mov     ebx, 2          ; fd
.text:0804905A                 mov     ecx, offset byte_804A024 ; addr
.text:0804905F                 mov     edx, 2          ; len
.text:08049064                 int     80h             ; LINUX - sys_read
.text:08049066                 mov     al, ds:byte_804A024
.text:0804906B                 sub     al, 30h
.text:0804906D                 mov     bl, ds:byte_804A025
.text:08049073                 sub     bl, 30h
.text:08049076                 adc     al, bl
.text:08049078                 daa
.text:08049079                 add     bl, 30h
.text:0804907C                 cmp     al, 16h
.text:0804907E                 jnz     short sub_8049000
.text:08049080                 cmp     bl, 38h
.text:08049083                 jnz     sub_8049000
.text:08049089                 cmp     eax, eax
.text:0804908B                 jz      short loc_804901D
.text:0804908B start           endp

```
This program is read the first bytes in al second in bl.
Analysis code from line 169 to 173 we can see : 
```
bl + 0x30 = 0x38
al + bl = 0x16

=> al = 0x8 , bl = 0x8
```


## nasm
Source code for this 
```
┌──(kali㉿kali)-[~/Rev/Release_1/nasm]
└─$ file nasm    
nasm: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), statically linked, not stripped

   0x0000000000401028 <+0>:     mov    eax,0x1
   0x000000000040102d <+5>:     mov    edi,0x1
   0x0000000000401032 <+10>:    movabs rsi,0x402000
   0x000000000040103c <+20>:    mov    edx,0x16
   0x0000000000401041 <+25>:    syscall 
   0x0000000000401043 <+27>:    mov    eax,0x0
   0x0000000000401048 <+32>:    mov    edi,0x0
   0x000000000040104d <+37>:    movabs rsi,0x402031
   0x0000000000401057 <+47>:    mov    edx,0x10
   0x000000000040105c <+52>:    syscall 
   0x000000000040105e <+54>:    movabs rdi,0x402026
   0x0000000000401068 <+64>:    movabs rsi,0x402031
   0x0000000000401072 <+74>:    mov    ecx,0xb
   0x0000000000401077 <+79>:    repz cmps BYTE PTR ds:[rsi],BYTE PTR es:[rdi]
   0x0000000000401079 <+81>:    je     0x401000 <correct_func>
   0x000000000040107b <+83>:    mov    eax,0x1
   0x0000000000401080 <+88>:    mov    edi,0x1
   0x0000000000401085 <+93>:    movabs rsi,0x40201f
   0x000000000040108f <+103>:   mov    edx,0x7
   0x0000000000401094 <+108>:   syscall 
   0x0000000000401096 <+110>:   mov    eax,0x3c
   0x000000000040109b <+115>:   mov    edi,0x0
   0x00000000004010a0 <+120>:   syscall 

```
Main flow is  compare string in 0x402026 vs 0x402031. If compare it jump to correct_func
```
pwndbg> x/s 0x402026
0x402026:       "supersecret"<error: Cannot access memory at address 0x402031>
```
We have password !


## Clone 

Check it!!
```
┌──(kali㉿kali)-[~/Rev/Release_1/clone]
└─$ file clone.exe 
clone.exe: PE32 executable (GUI) Intel 80386, for MS Windows
```
So now we know it a Window exec file 32 bits. Using IDA Pro 32bits no analysis :<<<<<<<

Flow of this is complicated .
```
(s[0] « 4 + s[1]) ^ 0x12 + 0x34

(s[2] « 4 + s[3]) ^ 0x56 + 0x78

(s[4] « 4 + s[5]) ^ 0x90 + 0xAB

(s[6] « 4 + s[7]) ^ 0xCD + 0xEF
```
