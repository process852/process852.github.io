# GDB 调试工具

## 常见使用的命令

* `list` 显示多行代码
* `info registers` 查看寄存器中保存的数据信息
* `disassemble 函数名` 查看函数的汇编代码
* `x /i $pc` 显示当前PC指向的指令
* `p $寄存器名字` 显示寄存器中的值
* `stepi` 单步执行一条汇编指令
* `x/a 地址值`用于查看内存地址中存放的另一个地址数值
* gdb设置汇编的显示风格
  * `set disassembly-flavor intel`
  * `set disassembly-flavor att`
* `x/nfu addr`检查内存地址addr处的n个单位，f表示格式(x表示16进制，d表示十进制)，u表示单位大小(b表示字节，w表示字)
  * `x/s addr`表示显示地址处的字符串
  * `x/13c addr`表示显示地址addr处开始的连续13个字符
  * `x/13d addr`表示显示地址addr处开始的13个字节，以十进制显示
* `p $eflags`可以查看条件标志位，`eflags`寄存器不同的位标识不同的标志位的状态
* `layout asm`调出两个窗口，一个显示汇编代码，一个显示gdb命令输入窗口