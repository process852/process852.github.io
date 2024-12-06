# 语言基本概念

## HelloWorld 程序

`java` 程序所有内容需要包含在类内实现。`javac` 是编译器，`java`是解释器。

* 编译命令 `javac -encoding UTF-8 HelloWorld.java`
* 执行上述命令后会生成 `HelloWorld.class` 文件
* 执行 `java HelloWorld` 控制台打印输出`HelloWorld`

```Java
// java 语言所有内容必须包括在类内
public class HelloWorld{
    // 代码执行由类内的 main 函数开始执行
    // 函数必须拥有返回类型
    public static void main(String[] args){
        // System.out.println 表示输出字符串
        System.out.println("Hello World!");
    }
}
```

## Strings



## 基本变量的声明

```java
int i = 0; // 需要显示声明变量的类型

```