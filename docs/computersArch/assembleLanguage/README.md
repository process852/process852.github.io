# 第一个汇编程序

```asm
;hello.asm
section .data
; msg 表示字符串的首地址
    msg db "hello, world", 0
section .bss
section .text
    global main
main:
    mov rax, 1
    mov rdi, 1
    mov rsi, msg
    mov rdx, 12
    syscall
    mov rax, 60
    mov rdi, 0
    syscall
```

## 汇编程序的结构

汇编程序主要包含三个部分：
* `.data`段
* `.bss`段
* `.text`段

#### .data段

数据段中使用如下方式声明和定义初始化数据，`<变量名称> <类型> <值>`。**变量名称**是指变量在内存中的起始位置。下表列出了可能的数据类型：

| 类型 | 长度 | 名称
| :---: | :---: | :---:
| db | 8 bits | Byte
| dw | 16 bits | Word
| dd | 32 bits | Double Word
| dq | 64 bits | Quad Word

`.data`段还可以包含常量，其声明格式为`<常量名称> equ <值>`。

```asm
section .data
    pi equ 3.1416
```

#### .bss段

`.bss`的全称为`Block Started by Symbol`。该段用于存储未初始化的变量，其声明格式如下`<变量名称>  <类型> <数字>`。bss 数据类型如下表所示：

| 类型 | 长度 | 名称
| :---: | :---: | :---:
| resb | 8 bits | Byte
| resw | 16 bits | Word
| resd | 32 bits | Double Word
| resq | 64 bits | Quad Word

```asm
section .bss
; 声明包含20个双字的数组dArray
    dArray resd 20
```

`.bss`段中的变量不包含任何值，**内存位置不是在编译时保留的，而是在执行时保留的**。

#### .txt段

`.txt`段是所有操作所在的位置。[linux系统调用链接](https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/)

## 二进制数、十六进制数以及寄存器

寄存器`rip`存储**下一条要执行的指令(该指令未被执行)**。

# 跳转和循环

## 跳转

```asm
; jump.asm

section .data
    number1 dq 42
    number2 dq 41
    fmt1 db "NUMBER1 > = NUMBER2", 10, 0
    fmt2 db "NUMBER1 < NUMBER2", 10, 0
section .bss
section .text
    global main
    extern printf
main:
    push rbp ; 栈帧指针入栈
    mov rbp, rsp ;
    mov rax, [number1]
    mov rbx, [number2]
    cmp rax, rbx ; 比较rax和rbx寄存器中的数据
    jge greater ; 若number1 大于等于 number2，则程序跳转至greater处继续执行

    mov rdi, fmt2 ;若number1 小于 number2，则执行此处内容
    mov rax, 0
    call printf
    jmp exit
greater:
    mov rdi, fmt1
    mov rax, 0
    call printf
exit:
    mov rsp, rbp
    pop rbp
    ret
```

## 循环

```asm
section .data
    number dq 5
    fmt db "The sum from 0 to %ld is %ld", 10, 0
section .bss
section .text
    extern printf
    global main
main:
    push rbp 
    mov rbp, rsp
    mov rbx, 0 ;计数器
    mov rax, 0 ; 用于存放累加和

jloop:
    add rax, rbx
    inc rbx
    cmp rbx, [number]
    jle jloop

    mov rdi, fmt
    mov rsi, [number]
    mov rdx, rax
    mov rax, 0
    call printf
    mov rsp, rbp
    pop rbp
    ret
```

* `loop` 指令比常规跳转指令耗时更长

```asm
section .data
    number dq 5
    fmt db "The sum from 0 to %ld is %ld", 10, 0
section .bss
section .text
    extern printf
    global main
main:
    push rbp 
    mov rbp, rsp
    mov rcx, [number] ;使用number初始化rcx
    mov rax, 0 ; 用于存放累加和

bloop:
    add rax,rcx
    loop bloop ;loop指令为循环指令，每次循环rcx减1，直到rcx为0停止

    mov rdi, fmt
    mov rsi, [number]
    mov rdx, rax
    mov rax, 0
    call printf
    mov rsp, rbp
    pop rbp
    ret
```