# Valgrind 工具得使用

Valgrind 包含了一系列工具套件，用于调式和侧写程序。

## Memcheck 工具

#### 示例代码

```C
#include <stdio.h>
#include <stdlib.h>

void f(void){
    int* x = (int *)malloc(10 * sizeof(int));
    x[10] = 0; // error 
}

int main(){
    f();
    return 0;
}
```

* `gcc -g -O0 example1.c -o example1` 编译时带有调试信息，可以方便valgrind给出错误的描述
* `valgrind --leak-check=yes {可执行文件名}(./example1)` 输出如下信息

```text
# 2774 表示Process ID
==2774== Memcheck, a memory error detector
==2774== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==2774== Using Valgrind-3.18.1 and LibVEX; rerun with -h for copyright info
==2774== Command: ./example1
==2774== 
# 无效的内存写入
==2774== Invalid write of size 4
==2774==    at 0x10916B: f (example1.c:6)
==2774==    by 0x109180: main (example1.c:10)
==2774==  Address 0x4a97068 is 0 bytes after a block of size 40 alloc'd
==2774==    at 0x4848899: malloc (in /usr/libexec/valgrind/vgpreload_memcheck-amd64-linux.so)
==2774==    by 0x10915E: f (example1.c:5)
==2774==    by 0x109180: main (example1.c:10)
==2774== 
==2774== 
==2774== HEAP SUMMARY:
==2774==     in use at exit: 40 bytes in 1 blocks
==2774==   total heap usage: 1 allocs, 0 frees, 40 bytes allocated
==2774== 
# 内存泄漏，未释放
==2774== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
==2774==    at 0x4848899: malloc (in /usr/libexec/valgrind/vgpreload_memcheck-amd64-linux.so)
==2774==    by 0x10915E: f (example1.c:5)
==2774==    by 0x109180: main (example1.c:10)
==2774== 
==2774== LEAK SUMMARY:
==2774==    definitely lost: 40 bytes in 1 blocks
==2774==    indirectly lost: 0 bytes in 0 blocks
==2774==      possibly lost: 0 bytes in 0 blocks
==2774==    still reachable: 0 bytes in 0 blocks
==2774==         suppressed: 0 bytes in 0 blocks
==2774== 
==2774== For lists of detected and suppressed errors, rerun with: -s
==2774== ERROR SUMMARY: 2 errors from 2 contexts (suppressed: 0 from 0)
```