- [一、数据类型](#一数据类型)
  - [1.1 数字类型](#11-数字类型)
  - [1.2 boolean 类型](#12-boolean-类型)
  - [1.3 字符串](#13-字符串)
    - [1.3.1 常见的转义字符](#131-常见的转义字符)
    - [1.3.2 字符串常见的操作](#132-字符串常见的操作)
  - [1.4 None](#14-none)
- [二、运算符](#二运算符)
  - [2.1 常用算术运算符](#21-常用算术运算符)
  - [2.2 比较运算符](#22-比较运算符)
  - [2.3 赋值运算符](#23-赋值运算符)
  - [2.4 位运算](#24-位运算)
  - [2.5 逻辑运算符](#25-逻辑运算符)
  - [2.6 成员运算符与身份运算符](#26-成员运算符与身份运算符)
- [三、控制语句](#三控制语句)
  - [3.1 if条件语句](#31-if条件语句)
  - [3.2 for循环](#32-for循环)
  - [3.3 while循环](#33-while循环)
- [四、数据结构](#四数据结构)
  - [4.1 列表 (List)](#41-列表-list)
  - [4.2 集合 (Set)](#42-集合-set)
  - [4.3 元组 (tuple)](#43-元组-tuple)
  - [4.4 字典 (dict)](#44-字典-dict)
  - [4.5 rang类型](#45-rang类型)
- [五、高级特性](#五高级特性)
  - [5.1 切片](#51-切片)
  - [5.2 列表生成式](#52-列表生成式)
  - [5.3 迭代](#53-迭代)
  - [5.4 生成器](#54-生成器)

# 一、数据类型

## 1.1 数字类型

- **Python中的数字类型支持哪几种数值？**

  **整型**：可正可负，不带小数点。在Python3中，整型没有大小限制，所以也可以存储长整型

  **浮点型**：可正可负，带小数点，可以使用科学计数法表示 1.1e2 = 110

  **复数**：复数由实数部分和虚数部分构成，可以用a + bj,或者complex(a,b)表示， 复数的实部a和虚

  部b都是浮点型，因用的较少，不做过多阐述，有兴趣可自行拓展

- **数字类型有什么特点**

  数字类型这种类型是**不可变的**，如果改变数字数据类型的值，将重新分配内存空间

```python
a = 1
print(int(a))
a = 2
print(int(a))
# int(a) != int(a)



a = 3
b = 3
print(int(a))
print(int(b))
# int(a) == int(b)
```

## 1.2 boolean 类型

在布尔类型一般用于表示条件是否成立，成立用True，不成立用False。**布尔类型是数字类型的一个子集**

```python
a = True
b = False
print(isinstance(a, int))
```

```python
print(bool(0))
print(bool(-1))
print(bool(0b10))
print(bool(''))

False
True
True
False
```

## 1.3 字符串

在Python中，使用双引号、单引号、三引号括起来的一系列字符就是字符串,无论是使用单引号还是双引号，都必须成对出现。

```python
"hello world"
'hello world'
'''hello world'''
```

Python 3版本中，所有的字符串都是使用**Unicode编码**的字符串序列

字符串的特性：**不可变**，如果改变字符串的值，相当于重新分配了空间

### 1.3.1 常见的转义字符

| 转义字符 | 含义         |
| -------- | ------------ |
| \a       | 发出系统铃声 |
| \\'      | 单引号       |
| \n       | 换行         |
| \\\      | 反斜杠       |
| \\"      | 双引号       |
| \b       | 退格         |
| \v       | 横向制表符   |
| \t       | 纵向制表符   |
| \r       | 回车         |
| \f       | 换页         |

### 1.3.2 字符串常见的操作

- **获取字符串中的某一部分**

| 操作                      | 输出              |
| ------------------------- | ----------------- |
| “my name is wiggin”[0]    | m                 |
| “my name is wiggin”[3]    | n                 |
| “my name is wiggin”[-1]   | n                 |
| “my name is wiggin”[-2]   | i                 |
| “my name is wiggin”[0:2]  | my                |
| “my name is wiggin”[0:-1] | my name is wiggi  |
| “my name is wiggin”[0:17] | my name is wiggin |
| “my name is wiggin”[0:22] | my name is wiggin |
| “my name is wiggin”[0:]   | my name is wiggin |
| "my name is wiggin"[:7]   | my name           |

- **字符串的格式化**

```python
s = "my name is %s and age is %d" %("xu", 24)
print(s)
```

**常用的格式化符号**

| 符号 | 作用                                 |
| ---- | ------------------------------------ |
| %c   | 格式化字符及其ASCII码                |
| %s   | 格式化字符串                         |
| %d   | 格式化整数                           |
| %f   | 格式化浮点数字，可指定小数点后的精度 |

## 1.4 None
- python中的None是一个特殊的常量。
- 它既不是0，也不是False，也不是空字符串。**它只是一个空值的对象**，也就是一个空的对象，只是没有赋值而已。
- None 可作为一个对象，该对象的类型为：NoneTye
- 它于其他编程语言中的 `Null` 一样
```python
a = None
b = None

# None
print(a)
# <class 'NoneType'>
print(type(a))

# 1796080848
print(id(a))
# 1796080848
print(id(b))

# a == b
if a == b:
    print("a == b")
else:
    print("a != b")

# a is b
if a is b:
    print(" a is b")
else:
    print(" a is not b")

# False
print(bool(a))
```


# 二、运算符

## 2.1 常用算术运算符

| 算术运算符 | 作用   |
| ---------- | ------ |
| +          | 加     |
| -          | 减     |
| *          | 乘     |
| /          | 除     |
| %          | 求模   |
| //         | 取整除 |
| **         | n次幂  |

## 2.2 比较运算符

| 比较运算符 | 作用                              |
| ---------- | --------------------------------- |
| >          | 大于                              |
| <          | 小于                              |
| ==         | 等于                              |
| !=         | 不等于                            |
| >=         | 大于等于                          |
| <=         | 小于等于                          |
| <>         | 不等于，作用同!=，在3.7版本已废弃 |

## 2.3 赋值运算符

| 赋值运算符 | 作用                     |
| ---------- | ------------------------ |
| =          | 直接赋值                 |
| +=         | 将加后的结果赋值自身     |
| -=         | 将减后的结果赋值自身     |
| *=         | 将乘后的结果赋值自身     |
| /=         | 将除后的结果赋值自身     |
| //=        | 将取整除后的结果赋值自身 |
| %=         | 将取模后的结果赋值自身   |
| **=        | 将幂运算后的结果赋值自身 |

## 2.4 位运算

| 位运算符 | 作用                                                         |
| -------- | ------------------------------------------------------------ |
| &        | 按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0 |
| \|       | 按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。 |
| <<       | 左移动运算符：运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数， 高位丢弃，低位补0。**乘与2的多少次幂** |
| >>       | 右移动运算符：把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数，**除2的多少次幂** |
| ~        | 按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1 |
| ^        | 按位异或运算符：当两对应的二进位相异时，结果为1              |

## 2.5 逻辑运算符

| 逻辑运算符 | 作用                                                         |
| ---------- | ------------------------------------------------------------ |
| and        | 表示与关系，前后均成立为真。对于x and y,如果 x 为 False，x and y 返回 x，否则它返回 y 的计算值。 |
| or         | 表示或关系，前后只要一个为真即为真。对于 x or y ，x如果 x 是非，它返回 x 的值， 否则它返回 y 的计算值 |
| not        | 表示非关系，后面条件不成立时为真。对于not x，如果 x 为 True，返回 False 。如果x 为 False，它返回 True。 |

## 2.6 成员运算符与身份运算符

| 成员运算符 | 作用              |
| ---------- | ----------------- |
| in         | 表示在xxx里面     |
| not in     | 表示不在xxx范围内 |
| is         | 是xxx             |
| is not     | 不是xxx           |

```python
a = '123'b = '12'
print(b in a)
True

a = '123'
b = '12'
print(b not in a)
False

a = '123'
b = '123'
print(b is a)
True

a = '123'
b = '123'
print(b is not a) False
```

**is 与 == 区别：**

is用于判断两个变量引用对象是否为同一个， == 用于判断引用变量的值是否相等。

```python
a = [1, 2, 3]
b = a[:] 
print(b is a) 
print(b == a)

False 
True
```

# 三、控制语句

## 3.1 if条件语句

```python
if a > b:
    print("hello")
elif a < b:
    print("world")
else:
    print("No")
```

## 3.2 for循环

```python
result = 0
for i in range(101):
    result = result + i
print(result)


demo_list = ["1", "2", "3", "4"]
for i in range(len(demo_list)):
    print(list[i])
```

## 3.3 while循环

```python
result = 0
i = 1
while i <= 100:
    result = result + i
    i = i + 1
else:
    print("no:", i)

print(result)
```

# 四、数据结构

## 4.1 列表 (List)

**特点：**

- 有序，放进去的顺序跟取出的顺序是一致的
- 可重复，成员可重复出现

**列表的常用操作：**

| 操作               | 说明                               |
| ------------------ | ---------------------------------- |
| list.append(obj)   | 在列表后面新增元素                 |
| del list[i]        | 删除元素                           |
| len(list)          | 求列表长度                         |
| list[i]            | 读取第i个元素                      |
| list[-i]           | 读取倒数第i个元素                  |
| list[i,j]          | 从第i个元素截取                    |
| list.index(objc)   | 从列表中找出某个值第一次出现的地方 |
| list.insert(i,obj) | 在第i个元素的位置插入元素          |
| list.pop(i)        | 移除第i个元素，并返回其值          |

## 4.2 集合 (Set)

**创建set：**

- 在Python中，使用大括号{  }或set()函数创建集合
- 当我们要创建一个空集合的时候，只能用set()进行创建，因为{ }表示的是空的字典集

**特点：**

- 成员无序，元素往set里存储前，会计算hash值，这个hash值决定了其存储的位置
- 成员不可重复出现（多次放入同一个元素，只算一个）

**集合常用操作：**

| 操作              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| set.add(item)     | 往集合里添加一个元素                                         |
| set.update(item)  | 往集合里添加元素，item是可迭代对象如：列表、元组、字典等     |
| set.remove(item)  | 将元素 item 从集合 set 中移除，如果元素不存在，则会发生错误。 |
| set.discard(item) | 将元素 item 从集合 set 中移除，如果元素不存在，不会发生错误  |
| set.pop()         | 随机取出并删除一个元素                                       |
| set.len()         | 计算集合个数                                                 |
| set.clear()       | 清空集合                                                     |
| union()           | 取两个集合的并集                                             |

## 4.3 元组 (tuple)

**创建元组：**

- 元组使用小括号( ),创建元组的时候，只要在括号中添加相应的元素，并使用逗号分隔即可
- 要创建一个只有一个元素的元组的时候，在元素后面要加一个逗号，如：tup =（1，）

**特点：**

- 元组与列表非常相似，不同之处在于元组的元素不能修改、整个元组也不能变动。

**元组常见操作**

| 操作         | 说明                     |
| ------------ | ------------------------ |
| 新增元素     | 不允许                   |
| 修改元素     | 不允许                   |
| 删除某个元素 | 不允许                   |
| tup[i]       | 获取第i个元素            |
| tup[-i]      | 获取倒数第i个元素        |
| tup[i:j]     | 从第i个元素起到第j个元素 |

**元组相关转换**
```python
#1、字典
dict = {'name': 'Zara', 'age': 7, 'class': 'First'}
#字典可以转为元组，返回：('age', 'name', 'class')
print tuple(dict)
#字典可以转为元组，返回：(7, 'Zara', 'First')
print tuple(dict.values())

#2、列表
nums=[1, 3, 5, 7, 8, 13, 20]
#列表转为元组，返回：(1, 3, 5, 7, 8, 13, 20)
print tuple(nums)

# 3、字符串
#字符串转为元组，返回：(1, 2, 3)
print tuple(eval("(1,2,3)"))


tup=(1, 2, 3, 4, 5)
#元组转为字符串，返回：(1, 2, 3, 4, 5)
print tup.__str__()
#元组转为列表，返回：[1, 2, 3, 4, 5]
print list(tup)
```

## 4.4 字典 (dict)

**创建字典：**

- 通过大括号{ }包裹

**特点：**

- 在字典中，key不能重复，如果放入相同的key，后者的值会覆盖前者
- 在字典中，key必须是不可变的

**字典常见操作：**

| 操作            | 说明                                       |
| --------------- | ------------------------------------------ |
| update({1:2})   | 新增元素                                   |
| dict['key']     | 通过key获取对应的值，如果没对应key，会报错 |
| dict['key']=123 | 修改key对应的值                            |
| del dict['key'] | 删除一个key及其对应value                   |
| del dict        | 清空整个字典                               |
| len(dict)       | 字典元素个数                               |
| pop('key')      | 删除字典给定键 key 及对应的值数,返回value    |

**字符串和字典之间相互转换**

```python
# 通过json做跳板进行转换
user  = '{"name":"jim","sex":"male","age":"18"}'
user_json = json.loads(user)

#  使用python3的内置函数
import ast
str_of_dict = "{'key1': 'key1value', 'key2': 'key2value'}"
result = ast.literal_eval(str_of_dict)
```

**判断python字典中key是否存在**
```python
user  = '{"name":"jim","sex":"male","age":"18"}'

# 方式一：
user.has_key("name")

# 方式二(建议)：
"name" in user.keys()
```

**字典之间的比较**
```python
# 没有嵌套字典
first_dict = {"name": "许","age": 22,"sex": "男",}
second_dict = {"name": "许","age": 22}

set1 = set(first_dict.items())
set2 = set(second_dict.items())
result = set1 ^ set2


if len(result) == 0:
  print("两个字典相同")
else:
  print("字典中不相同的属性", result)
  
```

## 4.5 rang类型

- `range()` 函数返回的是一个**可迭代对象（类型是对象）**，而不是列表类型， 所以打印的时候不会打印列表。

  ```python
  print(range(6))
  
  # 输出结果：	range(0, 6)
  ```

- 如果想把**range对象变成列表**，可以使用**list()函数对range进行处理**

  ```python
  print(list(range(6)))
  
  # 输出结果：	[0, 1, 2, 3, 4, 5]
  ```

- range函数的基本语法

  ```python
  '''
  range(stop)
  range(start, stop[, step])
  
  start: 计数从 start 开始。默认是从 0 开始。例如range（5）等价于range（0， 5）; 
  stop: 计数到 stop 结束，但不包括 stop。例如：range（0， 5） 是[0, 1, 2, 3, 4]没有5 
  step：步长，默认为1。例如：range（0， 5） 等价于 range(0, 5, 1)
  '''
  
  print(list(range(6)))
  # 输出结果： [0, 1, 2, 3, 4, 5]
  
  print(list(range(1,6)))
  # 输出结果： [ 1, 2, 3, 4, 5]
  
  print(list(range(1, 6, 2)))
  # 输出结果： [ 1, 3, 5]
  
  print(list(range(-11, -6)))
  # 输出结果： [-11, -10, -9, -8, -7]
  
  print(list(range(1, -6, -1)))
  # 输出结果： [1, 0, -1, -2, -3, -4, -5]
  
  ```


# 五、高级特性

## 5.1 切片

**带头不带尾**

对于一个列表L = [1, 2, 3, 4, 5, 6, 7, 8, 9]，我们使用切片来获取特定元素

- 获取第1个到第3个（数组下标从0开始，切片是左闭右开的区间，也就是包含0，不包含3)

  ```python
  L[0:3]
  ```

- 获取第2个到第五个

  ```python
  L[1:5]
  ```

- 取倒数第5个到倒数第2个

  ```python
  L[-5:-1]
  ```
- 取第2个到最后一个

  ```python
  L[3:]
  ```
- 前5个数，每2个取一个

  ```python
  L[:5:2]
  ```
- 所有数，每个两个取一个

  ```python
  L[::2]
  ```
## 5.2 列表生成式

**列表生成式：**

- `[expr for iter_var in iterable]`

- `[expr for iter_var in iterable if cond_expr]`

1. 生成一个10个元素的数据，每个分别对应1-10的两倍

```python
range_ = [x * 2 for x in range(1, 11)]
print(range_)
```

2. 生成一个100以内所有偶数的列表

```python
range_ = [x for x in range(1, 101) if x % 2 == 0]
print(range_)
```

3. 使用列表生成式生成[[1, 0], [1, 1], [1, 2], [1, 3], [1, 4], [1, 5], [2, 0], [2, 1], [2, 2], [2, 3], [2, 4], [2, 5]] 这样的列表

```python
list_ = [[x, y] for x in range(1, 3) for y in range(0, 6)]
print(list_)
```

## 5.3 迭代

**在Python中，只要是可迭代的对象，无论有没有下标，都可以进行迭代**

- 如何判断一个对象是不是可迭代的？

  ```python
  from collections.abc import Iterable
  
  print(isinstance('aaa', Iterable))
  ```

- 如果可迭代对象里的数据成对出现，想一次性遍历出两个对象，怎么办？

  ```python
  for x, y in [(1, 2), (4, 5)]: 
      print("x+y=", x + y)
  ```

## 5.4 生成器

通过列表生成式，可以直接创建一个列表，但是，受到内存的限制，列表容量是有限的，当列表元素很  大的时候，会很浪费内存空间。所以可以通过**生成器 Generator 生成**。

- `(expr for iter_var in iterable)`

- `(expr for iter_var in iterable if cond_expr)`

```python
generator = (x * 2 for x in range(1, 3))
print(type(generator))

for item in generator:
    print(item)
```

