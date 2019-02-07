---
title: Lua学习
date: 2017-12-24 19:13:24
tags:
---
# Lua

## 简介

- Lua是脚本型语言
  - 动态编译
  - 动态执行
    - 每次修改不需要重新编译链接执行
  - 运行时编译而并非运行前编译
- 是C语言编写的
- 速度比C语言快



## 特性

### Lua的Hello World



```lua
print("Hello world")
```



**Lua行末不要分号**

### Lua的括号



```lua
do
    ……
    ……
    ……
end
```



**Lua语言几乎用不到大括号，取而代之的是do…end**



### Lua的注释



``` lua
--这是一个注释
// 双斜杠不是注释了哦

--[[
这是一个多行注释哦
]]
/*
 这不是多行注释了哦
*/
```



**小心不要变成纯文本了**

```lua
--如果上面的多行注释没有写 双横线的话，就变成的纯文本赋值语句哦

a = [[<html><head></head><body></body></html>]]

-- 这个时候的 a 就是一个纯文本
```





### 数据类型

- Lua是动态类型，不需要定义就可以直接使用

```lua
a = "I'm a"
print("a is "..a)
```

- Lua的数据类型是动态可变的

- Lua的数据类型
  - 数字类型
    - 整型
    - 浮点型
    - long double 等 都是 数字类型，并没有明确划分
  - 字符串类型
  - thread类型
    - 线程也算是一个数据类型
  - function类型
    - 函数方法的数据类型
  - table
    - 数组，融合的链表和键值对等
  - 其他类型

```lua
a = function(x)
    print("user input is "..x)
end

a("test")
-- 这就相当于调用了function(x) 那个函数

-- 唯一一个使用了 大括号的地方
myTable = {12,13}
print(myTable) -- 会输出table的地址
for k,v in pairs(myTable) do
    print(k,v)
end
-- 输出了序列号和对应的值（序号从1开始）
```



### 变量作用域

```lua
b = "123"
local c = 12

local function myfuntion1()
    print("i'm lua")
end


local function myfuntion2()
  	local a = "hello"
    return a
end
```

- 其他lua文件引用该lua文件的时候，将无法访问到`local`标记的变量
- 相当于 是一个 private 的变量
- 反之 如果不加 `local`标识符，那么Lua默认的是全局变量`global`类型

**如果一个function函数中创建的变量不是local的，就意味着它是一个global变量**



### if语句(没有switch语句)

- 单独一个if

```lua
local a = 12
if a == 12 then
	print("a\'s value is 12")
end
```

- if..else 语句

```lua
local a = 2
if a == 2 then
    print("value is 12")
else 
    print("value is not 12")    
end
```



- if...else if...语句

```lua
local a = 12
if a == 12 then 
    print("value is 12")
    elseif a ~= 11 then
    print("value is not 11")
end
```

**这里不等于符号是 `~=` 注意注意！！！！！**



### 函数/方法

#### 无参无返回值

```lua
local function f1()
    print("hello")
end
```



#### 有参无返回值

```lua
local function f2(a)
    print(a)
end
```



#### 有参有返回值

```lua
local function f3(a)
    a += 2
	return a
end

--调用
a = f3(123)
```



#### 返回多个值

```lua
local function f4()
    return 1,2
end

-- 调用
local a,b = f4()
```



#### 可变参数列表

```lua
local function f5(...)
    local myTable = {...}
    
    for k,v in pairs(myTable) do
        print(k,v)    
    end
end

-- 调用
f5("12",123,"ok")
```



#### 库函数

- print() 就是一个很明显的print()，因为我们没有定义它
- 有些函数是Lua自带的



### 逻辑操作符

```lua
and or not
```

- 表示假
  - false
  - nil
- 表示真
  - 0
  - 其他数值

> and 和 or 就类似于 C语言中的 && 和 ||

- and
  - 如果我们第一个需要去计算的操作数，如果操作数是假，则返回第一个操作数
  - 反之则返回第二个操作数

```lua
print(1 and 2)
-- 输出的 2 哦
print(false and 5)
-- 输出 false 哦
```

- or
  - 如果第一个我们需要去计算你的操作数为真，返回第一个值
  - 反之返回第二个值

```lua
print(1 or 5)
-- 返回 1
print(false or 5)
-- 返回 5
```



> not 类似于 C语言的 ! 取反

- not 
  - 永远返回的是 true或false

```lua
print( not nil)
-- 返回 true
print( not 1)
-- 返回 false
```



### 循环语句



#### while



```lua
local index = 1
local mytable = {1,2,3}
while mytable[index] do 
    print(mytable[index])
    index = index+1
end
```



#### do……while换成了 repeat



```lua
repeat
    line = io.read() -- 从命令行获取输入
	print(line)
until line ~= ""
```



#### for循环

```lua
for i = 1, 5 do
	print(i)    
end
-- 输出 1 2 3 4 5 想想为什么

for i = 1, 10, 2 do
	print(i)    
end
-- 输出 1 3 5 7 9 想想为什么

for i = 20, 10, -2 do
	print(i)    
end
-- 输出 20 18 16 14 12 想想为什么

table = {1,2,3}
for i=1, #table do
    print(table[i])
end
-- #table 相当于取 table的长度，然后遍历
```



**上述可见，for 后面有三个参数 一个是初始化i，一个是结束判断，一个是加减i(默认为1)**



### Table的使用

- Table类似于Java的list和map的结合体



```lua
-- 建立一个有数值的table
local MyTable = {
    1, 			-- 索引为1
    2,			-- 索引为2
    3,			-- 索引为3
    4,			-- 索引为4
    5,			-- 索引为5
    table2 = {1,2,3}, -- 索引不为6
    "ok"		-- 索引为6
}

```

**为什么上面的table2的索引部位6呢？**



#### Table的遍历方式

- Table的复杂性导致其有三种遍历方式
- 因为Table既是链表类型又是键值对类型

```lua
myTable = {
    k = "x"
}
print(myTable[k])
-- 输出 nil
print(myTable["k"])
-- 输出 x
print(myTable.k)
-- 输出 x

-- 又或者直接
s = "ok"
myTable[s] = 10
print(myTable[s])
-- 直接通过键去设置值

```

**myTable.k 与 myTable["k"]有所不同**

- myTable.k 等价于 myTable["k"]，索引的键就变成了字符串
- myTable[k] 表示用变量k的值来索引table，索引的键可以是其他



#### 普通遍历方式

```lua
myTable={
    1,2,3,4,k = "ok",5
}

for i=1, #myTable do
    print("value is "..myTable[i])
end
-- 只输出1,2,3,4,5 哦， 因为 "ok" 的键为 "k"
```



#### for ipairs(迭代器)

```lua
for i,v in ipairs(myTable) do
    print(i,v)
end
```

**与第一种for循环方式一样，都是按照当前索引的隐式索引来迭代并显示值的**



#### for pairs(迭代器)

```lua
for k,v in pairs(myTable) do
    print(k,v)
end
```

**按照键值对来输出**

**如果值为一个table，则会输出该table的地址**



#### Table的作用

1. 你可以作为第三方插件集成到项目中，为项目提供一个支持功能
2. 完全使用table进行开发
3. 当做一种数据的配置集（就是阵列）


- 整体游戏的配置集（例子）


```lua

-- 使用lua，当做一种配置信息
application_config = {
    game_config = {
        ifDebugModel = false, -- 调试模式
        isCheatModel = true -- 作弊模式
    },

    sound_config = {
        isBackgroundMusicOpen = true,
        isEffectOpen = false
    },

    textrure_config = {
        Plist_Dictionary = "res/plist/",
        PACKE_TEXTURE_DIR = "res/images/"
    }
}

-- 小怪阵列
enemy_waves = {
    {enterId = 1, infoid = 1},
    {enterId = 2, infoid = 1},
    {enterId = 2, infoid = 2},
    {enterId = 1, infoid = 2},
    {enterId = 1, infoid = 1}
    --[[
        很典型的小怪阵列
        enterId 指的是 出兵口
        infoid 有一些具体信息
    ]]
}

enemy_datas = {
    { maxHp = 100, damage = 70, isHaveSpecialEffect = true },
    { maxHp = 50, damage = 20, isHaveSpecialEffect = false },
    { maxHp = 75, damage = 50, isHaveSpecialEffect = false },
    { maxHp = 125, damage = 80, isHaveSpecialEffect = true }
    -- 这里的参数 maxHp 指的是最高血量，damage 指的是攻击伤害， isHavaSpecialEffect 指的是是否有攻击特效
}


for key, value in pairs(enemy_datas) do
    print(key, value)
    if type(value) == "table" then
        for ik,iv in pairs(value) do
            print(ik, iv)
            print("__________")
        end
    end
end

```

**使用Lua可以很快的给角色赋予属性**
**使用Lua可以很快的设置调试属性**


### 读写数据文件

- 以万能的txt文件作为例子
- 这里使用IO库

#### 一种写法

- 读
```lua

local f = assert(io.open("123.txt",'r'))
--[[
    返回一个文件流指针
    assert 是一个断言，当读写输入报错的时候会报错
    这里的io其实是一个table，正如同上面的table所讲的使用 '.' 来获取键的值
    这里的open就是io的一个键
    open 函数 有两个参数 一个是 路径名字 一个是 操作名字

	r 以只读方式打开文件，该文件必须存在。
	
	w 打开只写文件，若文件存在则文件长度清为0，即该文件内容会消失。若文件不存在则建立该文件。
	
	a 以附加的方式打开只写文件。若文件不存在，则会建立该文件，如果文件存在，写入的数据会被加到文件尾，即文件原先的内容会被保留。（EOF符保留）
	
	r+ 以可读写方式打开文件，该文件必须存在。
	
	w+ 打开可读写文件，若文件存在则文件长度清为零，即该文件内容会消失。若文件不存在则建立该文件。
	
	a+ 与a类似，但此文件可读可写
	
	b 二进制模式，如果文件是二进制文件，可以加上b
	
	+ 号表示对文件既可以读也可以写
]]
local string = f:read("*all");
-- *all 表示读取文件的所有内容
--[[
	*line 表示读取一行
	*number 表示读取一个数字
	<num>	读取一个不超过num长度的字符串
]]
f:close() -- 关闭流
print(string)

```

**需要强调的是，f后面的':'相当于面向对象的封装方式**

-写

```lua

local function Write_txt(filename, inData)
    local f = assert(io.open(filename, 'a'))
    f:write(inData);
end

Write_txt("123.txt", "\nthis is a function");

```

#### 另一种写法

```lua

------------------简单模型-----------------
--读
local file1=io.input("1.txt")  --当前目录"1.txt"要存在，不然出错
local str=io.read("*a")
print(str)
--写
local file2=io.output("2.txt") --当前目录"2.txt"不需要存在
io.write(str)
io.flush()
io.close()

--利用这几个函数可以做一个文件复制的函数
function copy(fileA,fileB)
  local file1=io.input(fileA) 
  if not file1 then print(fileA.."不存在") return end
  local str=io.read("*a")
  local file2=io.output(fileB)
  io.write(str)
  io.flush()
  io.close()  
end

for line in io.lines("1.txt") do
  print(line)
end
------------------完整模型-----------------
local f=io.open("3.txt","a+")
f:write("Happy New Year!")
f:flush()

f:seek("end",-1) --定位到文件末尾前一个字节
local str=f:read(1) --读取一个字符
print(str) --输出"!"
f:close()

```

### 串行化
- 当一个对象没用被用到后就会从内存中delete掉，但是有的时候我们又想在之后恢复该对象到当时的状态

```lua

function serialize( o )

    if type(o) == "number" then
        io.write( o )
    elseif type(o) == "string" then
        io.write(string.format("%q", o))
    elseif type(o) == "table" then
        io.write("{\n")
        for k,v in pairs(o) do
            io.write("  ", k, " = ")
            serialize( v )
            io.write(",\n")
        end
        io.write("}\n")
    end
end

file = io.output("123.txt")
table = {
    1,2,3,4,5
}
serialize(table)
io.flush()
io.close()

```
**上述代码将一个table对象保存到txt文件中**

### 模块化 module

- Java有 package包 来封装类
- C++有 namespace 名空间 来封住类

## Lua与C++的交互

- Lua底层实现是 C/C++

### Lua与C++交互的中间件栈

- Lua与C++又部分不同，Lua有内部垃圾回收机制
- Lua无需声明直接使用，而C++需要声明变量


























