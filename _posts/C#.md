---
title: C#学习
date: 2017-12-22 19:14:38
tags:
---

# C#

## 数据类型

### 整型

- 整型即整数

- 整型可以分为有符号和无符号整行

  - 有符号整型

    - 可以表示负数和正数

    1. 字节型	sbyte
    2. 短整型    short 
    3. 整型        int
    4. 长整行    long

  - 无符号整型

    - 只能表示大于等于0的数

    1. 字节型    byte
    2. 短整型    ushort
    3. 整型	uint
    4. 长整型	ulong



- 有符号整型

| **整型** | **关键字** | **字节数** |   取值范围   |
| :------: | :--------: | :--------: | :----------: |
|  字节型  |   sbyte    |     1      |   -128~127   |
|  短整型  |   short    |     2      | -2^15~2^15-1 |
|   整型   |    int     |     4      | -2^31~2^31-1 |
|  长整型  |    long    |     8      | -2^63~2^63-1 |

- 无符号整型
| **整型** | **关键字** | **字节数** | 取值范围 |
| :------: | :--------: | :--------: | :------: |
|  字节型  |    byte    |     1      |  0~255   |
|  短整型  |   ushort   |     2      | 0~2^16-1 |
|   整型   |    uint    |     4      | 0~2^32-1 |
|  长整型  |   ulong    |     8      | 0~2^64-1 |



### 浮点型

- 单精度浮点型		float
- 双精度浮点型		double
- 高精度			decimal

| **浮点型** | **关键字** | **字节数** |
| :------: | :--------: | :--------: |
|  单精度  | float |     4     |
|  双精度  | double |     8     |
|   高精度   | decimal |     16     |

### 布尔型

- 布尔型    bool    1字节

- 只有两个值
  - true
  - false



### 字符型

- 字符型 char 两个字节





## 标识符

- 用来表示内存中的一个数据
- 一个由字符数据下划线和@符号组成的一个有序列



### 规则

1. 只能由数字字母下划线和@符号组成
2. 不能已数字开头
3. 如果包含@，那么@必须放在首位
4. 不能与关键字重名

```c#
xiaoming	符合
xiao_ming	符合
xiaoming_9	符合
_xiaoming	符合
xiaoming@163符合
1xiaoming	符合
INT			符合
```



### 规范

1. 望文知意

   - username	用户名

   - password	密码

   - ……这种

2. 遵循驼峰命名法

   1. 如果一个标识符由多个单词组成，那么单词首字母都要大写

      - UserName

      - UserID

   2. 如果一个标识符由多个单词组成，那么从第二个单词开始，后面的单词首字母大写

      - userName
      - userID

   3. 默认使用小驼峰




### 补充

-  标识符的组成部分也可以是汉字或者部分中文字符
- 不推荐使用汉字
- 少使用@来作为标识符的一部分

## 变量与常亮

- 如果一个标识符所表示的数据，在程序运行的过程中是可以被修改的，那么这个数据就是变量
- 程序运行中不能被修改的就是常亮 



```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsolApplication{
    class Program{
        static void Main(String[] args){
            Console.WriteLine("Hello World");
        }
    }
}
```



- using 表示应用命名空间
- namespace 表示命名空间
- class 代表一个类



## 代码语法

### 变量声明

#### 变量

```c#
// 数据类型 标识符 
int age;
long time;
bool flag = true;
age = 10;
time = 123412341234;
// 数据类型 标识符 = 初始值
int age = 10;
double pi = 3.1315926535;
// 声明多个变量
int length, width, height;
int length = 10, width = 10, height = 10;
```

#### 常量

- `必须声明的同时赋初值`
- `一旦声明，未来的代码中不能更改`



```c#
// const关键字声明常量
// 修饰的常量不能更改且必须赋初值
const int PI = 3.1415926535;
```



## 数据类型转换

- 数据类型转换并不是把一个变量的类型直接转换成其他的类型
- 是生命一个要转型的变量，然后将变量的值给这个新的类型的变量赋值



### 自动类型转换（隐式类型转换）

- 由数据范围小的数据类型转型为取值范围大的数据类型



```c#
// 自动类型转换的实例
sbyte num0 = 10;
int num1 = num0;
// 自动完成不需要额外操作
```



### 强制类型转换（显式类型转换）

- 由数据范围大的数据类型转换为取值范围小的数据类型
  - long -> int
  - int -> byte



```c#
// 强制类型转换
int num2 = 1111;
sbyte num3 = num2; // 此处会报错
sbyte num3 = (sbyte)num2; // 加上要转换的类型，强制类型转换
```

- sbyte 和 short 在参与运算的时候，会自动转成int型

```c#
sbyte n1 = 10, n2 = 20;
sbyte result = n1+n2; // 报错，因为上述的 sbyte 在参与运算的时候返回的是int型
sbyte result = (sbyte)(n1 + n2); // 对 
```

























