## Bash 基本概念和命令
Shell 脚本是一种为shell编写的脚本程序，Linux 的 Shell种类众多，常见的有：
* Bourne Shell（/usr/bin/sh或/bin/sh）
* Bourne Again Shell（/bin/bash）
* C Shell（/usr/bin/csh）
* ...
`#!/bin/bash`用于指定后续解释该程序所使用的shell程序。
* 第一个示例:`./test.sh`执行该脚本程序，由于默认新建文件没有可执行权限，需要使用命令`chmod +x ./test.sh`添加权限才可以正确执行。
```bash
#!/bin/bash

echo "Hello World!!!" # echo 会将后续的字符串输出到屏幕中
```
#### Shell 变量
变量是用于存储数据值的名称，如`your_name="runoob"`。与一般编程语言的区别是，**变量名和变量值之间的等号不可以有空格**。同时，变量名的命名规则需要遵守以下原则：
* 只包含字母、数字和下划线
* 不能以数字开头
* 避免使用 Shell 关键字
* 使用大写字母表示常量
* 避免使用特殊符
* 避免使用空格
**变量名的使用**
```bash
your_name="Runoob"
echo $your_name # 利用美元符号表示使用对应的变量名，{}表示界定变量名的范围
your_name="Jack" # 已定义的变量名可以重新赋值
echo ${your_name}
```
**只读变量**
使用`readonly`命令可以将变量定义为只读变量，其值不可以更改
```bash
#!/bin/bash
url="https://baidu.com"
readonly url
url="https://souhu.com" # 会报错
```
**删除变量**
使用`unset`命令可以删除变量,输出的删除变量名为空，但是运行不会报错
```bash
my_name='Jack'
unset my_name
echo ${my_name}
```
**变量类型**
* 字符串类型：使用`'`或`"`来定义
    - 单引号里任何字符都会原样输出，其变量是无效的
    - 双引号里可以有变量也可以有转义字符
    - `${#string}`获取字符串长度
    - `${string:1:4}`获取字符串的子串，索引为1到4的子串
* 整数类型：`declare -i my_integer=42`
* 数组变量：支持一维数组，但不支持多维数组。在shell中定义数组，用括号表示数组，数组元素用空格分割开来。
    - `${array_name[@]}`:`@`符号可以获取数组的所有元素
    - `${#array_name[@]}`:获取数组元素个数
    - `${#array_name[*]}`：获取数组元素个数
```bash
#!/bin/bash
my_array=(1,2,3,4,5) #整数索引数组
declare -A associative_array # 关联数组
associative_array["name"]="John"
associative_array["age"]=30
```
* 环境变量：由操作系统或用户设置的特殊变量，如`${PATH}`
* 特殊变量：
    - `$0`表示脚本名称
    - `$1，$2`表示脚本参数
    - `$#`表示传递给脚本的参数数量
    - `$?`表示上一个命令的退出状态