- [一、函数式编程](#一函数式编程)
  - [1.1 匿名函数lambda表达式](#11-匿名函数lambda表达式)
  - [1.2 高阶函数map](#12-高阶函数map)
  - [1.3 高阶函数reduce](#13-高阶函数reduce)
  - [1.4 高阶函数之ﬁlter](#14-高阶函数之ﬁlter)
  - [1.5 高阶函数之sorted](#15-高阶函数之sorted)
  - [1.6 闭包](#16-闭包)
  - [1.7 装饰器](#17-装饰器)
- [二、错误处理](#二错误处理)
  - [2.1 异常捕获和处理](#21-异常捕获和处理)
  - [2.2 自定义异常](#22-自定义异常)
- [三、IO操作](#三io操作)
  - [3.1 输入输出](#31-输入输出)
  - [3.2 文件的读取](#32-文件的读取)
  - [3.3 文件的写入](#33-文件的写入)
  - [3.4 操作文件夹](#34-操作文件夹)
  - [3.5 StringIO和BytesIO](#35-stringio和bytesio)
- [四、面向对象](#四面向对象)
  - [4.1 类和对象](#41-类和对象)
  - [4.2 构造函数](#42-构造函数)
  - [4.3 实例方法，类方法，静态方法](#43-实例方法类方法静态方法)
    - [实例方法：**](#实例方法)
    - [类方法](#类方法)
    - [静态方法](#静态方法)
  - [4.4 访问限制](#44-访问限制)
    - [4.4.1 设置访问限制](#441-设置访问限制)
    - [4.4.2 打破访问限制](#442-打破访问限制)
    - [4.4.3 @property装饰器](#443-property装饰器)
  - [4.5 继承](#45-继承)
    - [4.5.1 单继承](#451-单继承)
    - [4.5.2 多继承](#452-多继承)
    - [4.5.3 多重继承带来的问题](#453-多重继承带来的问题)
  - [4.6 super](#46-super)
  - [4.7 抽象方法与多态](#47-抽象方法与多态)
  - [4.8 枚举类](#48-枚举类)
- [五、网络编程](#五网络编程)
  - [5.1 socket](#51-socket)
  - [5.2 UDP](#52-udp)
  - [5.3 TCP](#53-tcp)
- [六、多线程和多进程](#六多线程和多进程)
  - [6.1 创建线程](#61-创建线程)
    - [6.1.1 通过`_thread`实现](#611-通过_thread实现)
    - [6.1.2 通过`threading`实现](#612-通过threading实现)
  - [6.2 线程安全问题](#62-线程安全问题)
  - [6.3 多进程](#63-多进程)

# 一、函数式编程

## 1.1 匿名函数lambda表达式

**基本格式：**

- `lambda 入参: 表达式`

匿名函数，顾名思义就是没有名字的函数，在程序中不用使用def进行定义，可以直接使用lambda关键字编写简单的代码逻辑。**lambda本质上是一个函数对象，可以将其赋值给另一个变量**，再由该变量来 调用函数，也可以直接使用。

```python
def power(x):
    x = x + 2
    return x

print(power(2))
```

使用lambda表达式的时候，我们可以这样操作

```python
power = lambda x: x + 2

print(power(2))
```

如果需要多个参数

```python
power = lambda x, n: x + n

print(power(2, 3))
```

## 1.2 高阶函数map

**map的基本格式：**

- `map(func, *iterables)`

map()函数接收两个以上的参数，开头一个是函数，剩下的是序列，**将传入的函数依次作用到序列的每个元素**，并把结果作为新的序列返回。

```python
def add(x):
	return x + 1

result = map(add, [1, 2, 3, 4]) 
print(type(result)) 
print(list(result))

# <class 'map'>
# [2, 3, 4, 5]
```

## 1.3 高阶函数reduce

**基本格式：**

- `reduce(function, sequence, initial=None)`

reduce把一个函数作用在一个序列上，这个函数必须接收两个参数，reduce函数把结果继续和序列的下一个元素做累积计算，**跟递归有点类似**，reduce函数会被上一个计算结果应用到本次计算中

```python
reduce(func, [1,2,3]) = func(func(1, 2), 3)
```

使用reduce函数，计算一个列表的乘积

```python
from functools import reduce

def func(x, y):
    return x * y

print(reduce(func,[1, 2, 3]))
```

## 1.4 高阶函数之ﬁlter

**基本格式：**

- `ﬁlter(function_or_None, iterable)`

ﬁlter顾名思义是过滤的意思，带有杂质的（非需要的数据），经过ﬁlter处理之后，就被过滤掉。ﬁlter()接收一个函数和一个序列。把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。

使用ﬁlter函数对给定序列进行操作，最后返回序列中所有偶数

```python
def fun(x):
    return x % 2 == 0

result = filter(fun, [1, 2, 3, 4, 5])
print(list(result))


print(list(filter(lambda x: x % 2 == 0, [1, 2, 3, 4, 5])))
```

## 1.5 高阶函数之sorted

**基本格式：**

- `sorted(iterable, key=None, reverse=False)`
- iterable -- 可迭代对象。
- key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
- reverse -- 排序规则，reverse = True 降序 ， reverse = False 升序（默认）

sorted从字面上就可以看去这是个用来拍序的函数，sorted 可以对所有可迭代的对象进行排序操作

```python
result = sorted([4, 1, 6, 5, 67, 23, 54, 12, 34])
print(result)

# [1, 4, 5, 6, 12, 23, 34, 54, 67]

result = sorted([4, 1, 6, 5, 67, 23, 54, 12, 34], reverse=True)
print(result)

# [67, 54, 34, 23, 12, 6, 5, 4, 1]

data = [["Python", 99], ["c", 88]]
print(sorted(data, key=lambda item: item[1]))

# [['c', 88], ['Python', 99]]
```

## 1.6 闭包

在万物皆对象的Python中,函数是否能作为函数的返回值进行返回呢

```python
def my_power(): 
	n = 2
	def power(x):
        return x ** n
return power

p = my_power() print(p(4))

# 16
```

```python
def my_power():
    n = 2
    def power(x):
        return x ** n
    return power

n = 3
p = my_power();
print(p(4))
```

我们可以看到，my_power函数在返回的时候，也将其引用的值（n）一同带回,n的值被新的函数所使用，这种情况我们称之为闭包

当我们把n的值移除到my_power函数外面，这个时候来看下计算结果

```python
n = 2
def my_power():

    def power(x):
        return x ** n
    return power

n = 3
p = my_power();
print(p(4))

# 64
```

**如何查看闭包呢：**

- ` __closure__ `
- 当结果不为none时，就是闭包

```python
def my_power():
    n = 2
    def power(x):
        return x ** n
    return power

n = 3
p = my_power();
print(p.__closure__)

# (<cell at 0x0000000001D39A98: int object at 0x000007FEE29A7120>,)
```

## 1.7 装饰器

装饰器模式（Decorator Pattern）允许向一个现有的对象添加新的功能，同时又不改变其结构。这种类型的设计模式属于结构型模式，它是作为现有的类的一个包装。装饰器的实现原理其实就是**闭包**

```python
def fun():
    print('这是一个函数')

fun()
```

要再打印“这是一个函数”前面在打印多一行hello world。

```python
# 看我们的装饰器函数my_wrapped，该函数接收一个参数func，其实就是接收一个方法名
# my_wrapped内部又定义一个函数inner，在inner函数中增加print
# 同时my_wrapped的返回值为内部函数inner，其实就是一个闭包函数。

def my_wrapped(func):
    def inner():
        print("hello world")
        func()

    return inner

# 在func上增加@my_wrapped，那这是什么意思呢？当python解释器执行到这句话的时候，会去调用my_wrapped函数，同时将被装饰的函数名作为参数传入(此时为func)
@my_wrapped
def func():
    print('这是一个函数')

func()
```

# 二、错误处理

## 2.1 异常捕获和处理

```
try:
    你要做的可能会发生异常的事
except 可能会发生的异常:
    发生异常之后要做的事
except 可能会发生的异常2:
    发生异常之后要做的事2
finally：
    最终要做的事情
```

```python
try:
    print(10/0)
except ZeroDivisionError:
    print("error")
finally:
    print("!")
```

## 2.2 自定义异常

- Python 允许我们在程序中手动设置异常，使用 `raise` 语句即可。

```python
class MYException(Exception):
    def __init__(self, parameter):
        err = '非法入参{0}'.format(parameter)
        Exception.__init__(self, err)
        self.parameter = parameter

def fun(x):
    if x == 0:
        raise MyException
    else:
        print(10/x)

fun(2)
fun(0)
```

# 三、IO操作

## 3.1 输入输出

```python
print("请输入内容，按回车键结束：")
str = input()
print("您输入的内容是：", str)
```

## 3.2 文件的读取

- 在python里面，可以使用**open函数**来打开文件

```
open(filename, mode)

filename：文件名，一般包括该文件所在的路径
mode 模式
如果读取时读取中文文本，需要在打开文件的时候使用encoding指定字符编码为utf-8
```

常见的打开文件的模式有:

| 模式 | 描述                                                         |
| ---- | ------------------------------------------------------------ |
| t    | 文本模式 (默认)。                                            |
| x    | 写模式，新建一个文件，如果该文件已存在则会报错。             |
| b    | 二进制模式。                                                 |
| +    | 打开一个文件进行更新(可读可写)。                             |
| r    | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。 |
| rb   | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一 般用于非文本文件如图片等。 |
| r+   | 打开一个文件用于读写。文件指针将会放在文件的开头。           |
| rb+  | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文 件如图片等。 |
| w    | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内 容会被删除。如果该文件不存在，创建新文件。 |
| wb   | 以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编 辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片 等。 |
| w+   | 打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容 会被删除。如果该文件不存在，创建新文件。 |
| wb+  | 以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编   辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片 等。 |
| a    | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说， 新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
| ab   | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结   尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进 行写入。 |
| a+   | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时 会是追加模式。如果该文件不存在，创建新文件用于读写。 |
| ab+  | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结 尾。如果该文件不存在，创建新文件用于读写。 |

- 读取文件的内容，使用read相关方法

使用read方法，读取文件的全部内容（如果文件较大，一次性读取可能会导致内存不足），此时需要指定使用readline方法，读取文件的一行

```python
filepath = "C:\\Users\\abc\\Desktop\\test.txt"
file = open(filepath, 'r', encoding='utf-8')
content = file.readline()
print(content)
```

每次打开文件完成相应操作之后，都必须关闭该文件，且因为文件在读写过程中可能出现IOError  而导致文件不能正常关闭，所以每次读写文件时，必须使用try   ﬁnally语法包裹，使其最终都能正常关闭文件

```python
try:
    filepath = "C:\\Users\\abc\\Desktop\\test.txt"
    file = open(filepath, 'r', encoding='utf-8')
    content = file.readline()
    print(content)
except:
    raise
finally:
    file.close()
```
如果觉得每次try ﬁnally语法不太优雅，可以使用python提供的另外一种方式:
```python
with open("C:\\Users\\abc\\Desktop\\test.txt", "r", encoding="utf-8") as file:
    print(file.readline()) 
    print(file.read())
```

## 3.3 文件的写入

```python
try:
    filepath = "C:\\Users\\abc\\Desktop\\test.txt"
    file = open(filepath, "a", encoding="utf-8")
    file.write("nihao")
except IOError:
    raise
finally:
    file.close()
```


## 3.4 操作文件夹

- **创建文件夹：**

在当前的目录下创建一个文件夹

```python
import os

os.mkdir("test")
```

创建一个多级文件夹

```python
import os

os.makedirs("test\\my")
```

- **获取当前文件夹：**

```python
import os

print(os.getcwd())
```

- **改变当前的工作目录**

```python
import os

os.chdir("test") 
print(os.getcwd())
```

- **删除空文件夹**

```python
import os

os.rmdir("test")
```

- **删除多层空文件夹**

```python
import os

os.removedirs("test\\my")
```

## 3.5 StringIO和BytesIO

我们更多接触到IO操作，都是在文件层面上进行操作。但是，在平时的开发中，在某些场景下，我们只是要缓存相应的文本内容，方便后续处理，此时，我并不需要往新建文件并写入，我只想直接在内存中缓存这些文本，此时StringIo，BytesIo就派上用场了。

- **StringIO**

```python
from io import StringIO

string_io = StringIO("HELLO WORLD")
print(string_io)
print(string_io.readline())
string_io.close()

# <_io.StringIO object at 0x0000000002139318>
# HELLO WORLD

string_io = StringIO()
string_io.write("hello world")
print(string_io.getvalue())
string_io.close()

# hello world


with StringIO() as str_io: 
    str_io.write("hello") 
    str_io.write("world") 
    print(str_io.getvalue())

# hello world
```

- **BytesIO**

```python
from io import BytesIO

byte_io = BytesIO("HELLO WORLD".encode('utf-8'))
print(byte_io)
print(byte_io.getvalue())
byte_io.close()

# <_io.BytesIO object at 0x0000000001DDA228>
# b'HELLO WORLD'


byte_io = BytesIO("你好世界".encode('utf-8'))
print(byte_io.getvalue())
byte_io.close()

# \xe4\xbd\xa0\xe5\xa5\xbd\xe4\xb8\x96\xe7\x95\x8c

print(str(b'\xe4\xbd\xa0\xe5\xa5\xbd\xe4\xb8\x96\xe7\x95\x8c','utf-8'))

# 你好世界
```

# 四、面向对象

## 4.1 类和对象

- 定义类的时候，类名需使用**驼峰的命名方式**，即单词首字母大写，如果类名由多个单词组成，同样每个单词的首字母都大写

```python
# 定义person类
class person():
    
    # 所有类方法，无论是否要用到，都必须有self参数
    def introduce_self(self):
        print("my name is wiggin")
        
# 实例化对象的时候 使用类名(),即可完成实例化
person = Person() 
# 调用对象方法可以使用对象名.方法名() 
person.introduce_self()
```

## 4.2 构造函数

- 构造函数 ，是一种特殊的方法。主要用来在创建对象的时候去**初始化对象**， 即为对象成员变量赋初始值
- python中**不支持多个构造函数**
- 使用`__init__` 作为构造函数，如果不显式写构造函数，python会自动创建一个啥事不干的默认构造函数

```python
# 定义person类 
class Person(): 
    def __init__(self): 
        print("hello world")
```

```python
class Person(): 
    # 作为模板，在构造函数中，为必须的属性绑定对应的值 
    def __init__(self, name, age, height): 
        self.name = name 
        self.age = age 
        self.height = height 
        
    def introduce_self(self): 
        print("hello,my name is %s,my age is %d and i'm %d height" % (self.name, self.age, self.height))
        
# 实例化对象的时候 使用类名(),即可完成实例化 
person = Person('tomcat', 11, 11) 
# 访问对象属性可以使用对象实例.属性名的方式为属性赋值 # 调用对象方法可以使用对象名.方法名() 
person.introduce_self()
```

当使用了构造函数，且构造函数式带参的且无默认参数，此时，实例化对象的时候，必须显式入参，否则会报错。若要避免错误，可以在构造函数使用默认参数

```python
# 定义person类 
class Person(): 
    # 作为模板，在构造函数中，为必须的属性绑定对应的值 
    def __init__(self, name, age, height): 
        self.name = name 
        self.age = age 
        self.height = height 
        
    def introduce_self(self): 
        print("hello,my name is %s,my age is %d and i'm %d height" % (self.name, self.age, self.height)) 
        
# 实例化对象的时候 使用类名(),即可完成实例化 
person = Person() 
# 访问对象属性可以使用对象实例.属性名的方式为属性赋值 # 调用对象方法可以使用对象名.方法名() 
person.introduce_self()
```

## 4.3 实例方法，类方法，静态方法

**self**：self指向实例本身

### 实例方法：**

与实例变量类似，属于实例化之后的对象，**定义实例方法至少要有一个self入参**，调用是不需要传，只能由实例对象调用。

```python
class Animal():

    def __init__(self, age, name):
        self.name = name
        self.age = age

    def eat(self):
        print(self.name, "is eating")


# 创建实例
animal = Animal("12", "Tom")
# 调用实例方法
animal.eat()
```

### 类方法

类方法使用装饰器`@classmethod`。第一个参数必须是当前类对象，该参数名一般约定为“cls”（不是cls也没关系，但是，约定俗成的东西不建议变动），通过它来传递类的属性和方法（不能传实例的属性和方法）；其调用对象可以是实例对象和类

```python
class Person():

    total = 0

    def __init__(self, age=0, name=''):
        self.name = name
        self.age = age

    """
    使用装饰器修饰
    cls 和 self 一样，但是约定俗成
    类方法的主要作用是操作类变量的
    """
    @classmethod
    def print_total(cls):
        cls.total += 1
        print(cls.total)

# 直接调用
Person.print_total()

# 通过实例调用（不建议）
person_one = Person()
person_one.print_total()
```

### 静态方法

使用装饰器 `@staticmethod`。参数随意，没有“self”和“cls”参数，但是方法体中不能使用类或实例的任何属性和方法；

静态方法是类中的函数，不需要实例。静态方法主要是用来存放逻辑性的代码，逻辑上属于类，但是和类本身没有关系，也就是说在静态方法中，不会涉及到类中的属性和方法的操作。可以理解为，静态方法是个独立的、单纯的函数，它仅仅托管于某个类的名称空间中，便于使用和维护。

```python
class person():

    @staticmethod
    def print_hello():
        print("hello world")


person.print_hello()
```

## 4.4 访问限制

### 4.4.1 设置访问限制

定义私有变量，我们定义了一个类，实例化了一个对象，给其年龄赋值-1，程序正确运行，但是，这不符合现实生活中的场景。当我们不加限制的将属性暴露出去，也就是意味着我们的类失去了安全性。

当我们不希望外部可以随意更改类内部的数据，可以将变量定义为私有变量，并提供相应的操作方法为了保证外部不可以随意更改实例内部的数据，可以在构造函数中，在属性和方法的**名称前加上两个下划线**，这样改属性就变成了一个私有变量，只有内部可以访问，外部不能访问。

```python
class Person():

    def __init__(self, age=0, name=''):
        self.name = name
        self.__age = age

    def introduce(self):
        print("my name is " + self.name + ",and age is " + str(self.__age))

    def __print_age(self):
        print("age is" + str(self.__age))


person = Person(10, 'Tom')
# 无法访问age这个属性
print(person.age)
print(person.__age)
# 无法调用改方法
person.__print_age()
```

### 4.4.2 打破访问限制

如下的一个python代码，最后的输出值为 -1 ，为什么私有方法被访问，还可以被赋值？
但是，Python并没有从语法上严格保证私有属性或方法的私密性，它只是给私有的属性和方法换了一个名字来妨碍对它们的访问，事实上如果你知道更换名字的规则仍然可以访问到它们

```python
# 定义person类
# 定义person类
class Person():

    # 构造函数，用于为成员变量赋初始值
    def __init__(self, name, age, height):
        self.name = name
        self.__age = age
        self.height = height

    def set_age(self, age):
        if age < 0 or age > 150:
            raise Exception("非法入参，年龄不合法")
        self.__age = age

    def introduce_self(self):
        print("hello,my name is %s,my age is %d and i'm %d height" % (self.name, self.__age, self.height))


person = Person("tom", 11, 111)
person.__age = -1
print(person.__age) 
person.introduce_self()

# -1
# hello,my name is tom,my age is 11 and i'm 111 height
```

**原因：** 在实例里面，python代码自动帮我们添加了一个_age的属性

```python
print(person. dict )

# {'name': 'tom', '_Person__age': 11, 'height': 111, '__age': -1}
```

通过dict的属性我们可以看到，私有的age其实是被换了一个名字，如果想要访问私有属性

```python
person = Person("tom", 11, 111)
person._Person__age = 12
print(person._Person__age)
person.introduce_self()
```
### 4.4.3 @property装饰器
之前我们讨论过Python中属性和方法访问权限的问题，虽然我们不建议将属性设置为私有的，但是如果直接将属性暴露给外界也是有问题的，比如我们没有办法检查赋给属性的值是否有效。我们之前的建议是将属性命名以单下划线开头，通过这种方式来暗示属性是受保护的，不建议外界直接访问，那么如果想访问属性可以通过属性的getter（访问器）和setter（修改器）方法进行对应的操作。如果要做到这点，就可以考虑使用@property包装器来包装getter和setter方法，使得对属性的访问既安全又方便。
```python
class Person:

    def __init__(self, name, age):
        self._name = name
        self._age = age

    # 访问器 - getter方法
    @property
    def age(self):
        return self._age

    # 修改器 - setter方法
    @age.setter
    def age(self, age):
        self._age = age

    def play(self):
        if self._age <= 16:
            print('%s正在玩飞行棋.' % self._name)
        else:
            print('%s正在玩斗地主.' % self._name)


def main():
    person = Person("李元芳", 12)
    person.play()
    person.age = 20
    person.play()


if __name__ == '__main__':
    main()
```

### 4.4.4 __slots__
一般情况下，Python允许在程序运行时给对象绑定新的属性或方法。但是，如果我们要限定自定义类型的对象只能绑定某些属性，可以通过在类中定义__slots__变量来进行限定，这相当于告诉解释器，实例的属性都叫什么，并且只能有这些属性，在定义时，**推荐__slots__使用元组，而不是列表，这样做可以节省内存, __slots__的限定只对当前类的对象生效，对子类并不起任何作用。**
```python
class Person:

    __slots__ = ("_name", "_age")

    def __init__(self, name, age):
        self._name = name
        self._age = age

    # 访问器 - getter方法
    @property
    def age(self):
        return self._age

    # 修改器 - setter方法
    @age.setter
    def age(self, age):
        self._age = age

    def play(self):
        if self._age <= 16:
            print('%s正在玩飞行棋.' % self._name)
        else:
            print('%s正在玩斗地主.' % self._name)


def main():
    person = Person("李元芳", 12)
    person.__dict__["pid"] = "001"
    # 报错，在person中已经约定了属性，无法再绑定新的属性

if __name__ == '__main__':
    main()
```

## 4.5 继承

### 4.5.1 单继承 

- 在定义类的时候，类名后有个括号，当括号里写着另外一个的名字时，表示该类继承于另外一个类
- 子类可以有自己的属性和方法
- 当子类有自己的构造时会覆盖父类的构造
- 当子类有和父类一样的方法（名称和入参）会将父类的方法**重写**

```python
class Animal():

    def __init__(self, name):
        self.name = name

    def eat(self):
        print(self.name + "is eating")

class Dog(Animal):
    
    def bark(self):
        print(self.name + " is barking")

class Cat(Animal):
    pass


dog = Dog("Tom")
dog.eat()
dog.bark()
cat = Cat("Jon")
cat.eat()
```

### 4.5.2 多继承

- python里面支持多重继承,与java不同
- 当继承多个父类时，如果父类中有相同的方法，那么**子类会优先使用最先被继承的方法**

```python
class Father:
    def power(self):
        print("拥有很大的力气")

class Mother:
    def sing(self):
        print("唱歌")

class Son(Father, Mother):
    pass

son = Son()
son.sing()
son.power()
```

### 4.5.3 多重继承带来的问题

**新式类与旧式类：**

- 新式类都从object继承（python3中，默认都继承自object），经典类不需要继承自object。
- 新式类的MRO(method resolution order 基类搜索顺序)算法采用C3算法**广度优先搜索**
- 旧式类的MRO算法是采用**深度优先搜索**
- 新式类相同父类只执行一次构造函数，经典类重复执行多次
- 查看继承顺序的代码 `类名.mro()`

```python
class Father:
    def my_fun(self):
        print("Father")


class Son1(Father):
    def my_fun(self):
        print("Son1")


class Son2(Father):
    def my_fun(self):
        print("Son2")


class Grandson(Son1, Son2):
    def my_fun(self):
        print("Grandson")


d = Grandson()
print(Grandson.mro())
d.my_fun()

# 在新式类中对my_fun的查询顺序为Son1 -> Son2 -> Father
# 在旧式类中对my_fun的查询顺序为Son1 -> Father -> Son2
```

**菱形继承 （钻石继承）**

我们之前学习继承的时候说过，要执行父类构造有两种方式，一种是直接使用父类名字调用构造，一种  是使用super(),我们说过，普通的继承中，这两种方法没啥大问题，但是，如果在多重继承里，使用父类名字调用构造可能会发生问题

**上层的构造方法被多次执行，造成资源的大量消耗**

```python
class Father:

    def __init__(self):
        print("father init")

    def my_fun(self):
        print("Father")


class Son1(Father):

    def __init__(self):
        Father.__init__(self)
        print("son1 init")

    def my_fun(self):
        print("Son1")


class Son2(Father):

    def __init__(self):
        Father.__init__(self)
        print("son2 init")

    def my_fun(self):
        print("Son2")


class Grandson(Son1, Son2):

    def __init__(self):
        Son1.__init__(self)
        Son2.__init__(self)
        print("Grandson init")

    def my_fun(self):
        print("Grandson")


d = Grandson()
d.my_fun()


# father init
# son1 init
# father init
# son2 init
# Grandson init
# Grandson
```

解决方式：

```python
class Father:

    def __init__(self):
        print("father init")

    def my_fun(self):
        print("Father")


class Son1(Father):

    def __init__(self):
        super().__init__()
        print("son1 init")

    def my_fun(self):
        print("Son1")


class Son2(Father):

    def __init__(self):
        super().__init__()
        print("son2 init")

    def my_fun(self):
        print("Son2")


class Grandson(Son1, Son2):

    def __init__(self):
        super().__init__()
        print("Grandson init")

    def my_fun(self):
        print("Grandson")


d = Grandson()
d.my_fun()

# father init
# son2 init
# son1 init
# Grandson init
# Grandson
```

## 4.6 super

**super的基本语法：**`super(类名, self)`

***super()***  函数是用于调用父类(超类)的一个方法。一般是用来解决多重继承问题的，直接用类名调用父类方法在使用单继承的时候没问题，但是如果使用多继承，会涉及到查找顺序（MRO）、重复调用（钻 石继承）等种种问题。

```python
class Animal:

    def __init__(self, name):
        self.name = name

    def eat(self):
        print(self.name + "is eating")

class Dog(Animal):

    def __init__(self):
        super(Dog, self).__init__("Dog")
        print("Dog")

dog = Dog()
dog.eat()
```

## 4.7 抽象方法与多态

**抽象方法：**

​		在面向对象编程语言中抽象方法指一些只有方法声明，而没有具体方法体的方法。抽象方法一般  存在于抽象类或接口中。抽象类的一个特点是它不能直接被实例化，子类要么是抽象类，要么，  必须实现父类抽象类里定义的抽象方法

**定义抽象方法：**

- 在python3中可以通过使用abc模块轻松的定义抽象类
- `from abc import ABCMeta, abstractmethod`

```python
from abc import ABCMeta, abstractmethod

class Animal(metaclass=ABCMeta):

    @abstractmethod
    def eat(self):
        pass

class Dog(Animal):

    def eat(self):
        print("Dog is eating")

dog = Dog()
dog.eat()
```

**什么是多态：**

不同的子类对象调用相同的父类方法，产生不同的执行结果，可以增加代码的外部调用灵活度。

## 4.8 枚举类

**枚举：**

在数学和计算机科学理论中，一个集的枚举是列出某些有穷序列集的所有成员的程序，或者是一种特定类型对象的计数。这两种类型经常（但不总是）重叠。

```python
# 1 红色 2：黄	3：绿
def judge(color):
    if color == 1 or color == 2:
        print("司机创红灯")
    else:
        print("司机正常行驶")
```

> 程序是我写的，我自己能理解。但是，如果别人来看我的程序，会  无法理解1跟2这两个数字的意义，这里有注释还好，但是还有一个问题，可能另外的同事1是表示绿   灯，这个时候双方理解就会产生很大的问题。

**枚举所使用的包：**

- `from enum import Enum, unique`

```python
class TrafficLight(Enum):
    RED = 1
    YELLOW = 2
    GREEN = 3


# 1 红色 2：黄	3：绿
def judge(color):
    if color == TrafficLight.RED or color == TrafficLight.YELLOW:
        print("司机创红灯")
    else:
        print("司机正常行驶")

judge(TrafficLight.YELLOW)
```

# 五、网络编程

## 5.1 socket

**官方定义：**

​		套接字（socket）是一个抽象层，应用程序可以通过它发送或接收数据，可对其进行像对文件一样的打开、读写和关闭等操作。套接字允许应用程序将I/O插入到网络中，并与网络中 的其他应用程序进行通信。网络套接字是IP地址与端口的组合。

**在python里面，提供了两个级别访问的网络服务**

- 低级别的网络服务支持基本的 Socket，它提供了标准的 BSD Sockets API，可以访问底层操作系统Socket接口的全部方法。
- 高级别的网络服务模块 SocketServer， 它提供了服务器中心类，可以简化网络服务器的开发。

## 5.2 UDP

UDP（User Data Protocol，用户数据报协议）是无连接的，即发送数据之前不需要建立连接， UDP尽最大努力交付，即不保证可靠交付（类似于发短信，我只管发，能不能接受到跟我关系不大）

> socket.socket(family,type,proto)
>
> family: 套接字家族可以使AF_UNIX或者AF_INET
>
> type: 套接字类型可以根据是面向连接(TCP)的还是非连接分(UDP)为SOCK_STREAM 或SOCK_DGRAM
>
> protocol: 一般不填默认为0
>
> AF_INET需经过多个协议层的编解码，消耗系统cpu，并且数据传输需要经过网卡，受到网卡带宽的限制。
>
> AF_UNIX数据到达内核缓冲区后，由内核根据指定路径名找到接收方socket对应的内核     缓冲区，直接将数据拷贝过去，不经过协议层编解码，节省系统cpu，并且不经过网卡，因此不   受网卡带宽的限制。
>
> AF_UNIX的传输速率远远大于AF_INET
>
> AF_INET不仅可以用作本机的跨进程通信，同样的可以用于不同机器之间的通信，其就是为了在不同机器之间进行网络互联传递数据而生。而AF_UNIX则只能用于本机内进程之间的通信。

**服务端：**

```python
import socket

# 创建一个socket
server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
# 绑定端口进行监听
server.bind(("127.0.0.1", 8888))
print("UDP 服务端启动")

while True:
    # 接收到信息，信息里面包括客户端发送的内容以及客户端的信息(ip，端口)
    data, client = server.recvfrom(1024)
    print("接受到客户端发来的消息：", data.decode('utf-8'))
    server.sendto("您好，这是服务端".encode("utf-8"), client)
```

**客户端：**

```python
import socket

# 创建一个socket
client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# 绑定端口进行发送
client.sendto("您好，我是客户端".encode('utf-8'), ("127.0.0.1", 8888))
# 接受服务端的消息
data, server = client.recvfrom(1024)
print(data.decode("utf-8"))
client.close()
```

## 5.3 TCP

TCP(Transmission Control Protocol传输控制协议）是一种面向连接的，可靠的，基于字节流的传输通信协议

**服务端：**

```python
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(("127.0.0.1", 8888))
server.listen(5)
print("服务端已经启动，等待客户端连接======》")
client, address = server.accept()
print("已经建立连接")
data = client.recv(1024)
print("服务端接收到的数据：", data.decode("utf-8"))
print(" 请 输 入 回 复 的 内 容 ：")
client.send(input().encode("utf-8"))
server.close()
```

**客户端：**

```python
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(("127.0.0.1", 8888))
print("客户端已启动，已完成连接")
print("请输入要发送的内容：")
client.send(input().encode("utf-8"))
data = client.recv(1024)
print("接收到服务端的响应：", data.decode("utf-8"))
client.close()
```

# 六、多线程和多进程

- python中的GIL详解(https://www.cnblogs.com/SuKiWX/p/8804974.html)
- 线程扩展阅读(https://www.cnblogs.com/hwlong/p/8952510.html)

在python的种，多线程是通过并发进行实现的。
> 并行是指两个或者多个事件在同一时刻发生；而并发是指两个或多个事件在同一时间间隔发生。

## 6.1 创建线程

### 6.1.1 通过`_thread`实现
`_thread` 有一个缺点，当主线程结束的时候，它所有的子线程都会强行结束
```python

def loop0():
    print("loop0 start " + ctime())
    sleep(4)
    print("loop0 end " + ctime())


def loop1():
    print("loop1 start " + ctime())
    sleep(2)
    print("loop1 end " + ctime())


def main():
    _thread.start_new_thread(loop0, ())
    _thread.start_new_thread(loop1, ())
    sleep(1)

# 当main函数执行结束后，会将loop0，loop1 两个子线程也进行强行停止，不会进行等待
if __name__ == "__main__":
    main()   
```
如果想要解决上述问题，需要手动添加锁，并对锁进行监听。
```python
import _thread
from time import ctime, sleep


def loop(num, sec, lock):
    print("loop", num, " start " + ctime())
    sleep(sec)
    print("loop", num, "  end " + ctime())
    lock.release()


def main():
    loops = [4, 2]
    locks = []
    num = range(len(loops))
    for i in num:
        # 声明一个锁，并将锁给锁上
        lock = _thread.allocate_lock()
        lock.acquire()
        locks.append(lock)
    for i in num:
        # 不将这个放入上一个循环的原因：获取锁也需要时间，可能会出现bug
        _thread.start_new_thread(loop, (i, loops[i], locks[i]))
    for i in num:
        while locks[i].locked():
            pass


if __name__ == "__main__":
    main()
```

### 6.1.2 通过`threading`实现
**方式一：**

```python
import threading

# 继承 threading.Thread，并重写run方法
class MyThread(threading.Thread):

    def run(self):
        print("hello world")


my_thread1 = MyThread()
my_thread2 = MyThread()
my_thread3 = MyThread()

my_thread1.start()
my_thread2.start()
my_thread3.start()
```

**方式二：**

> 参数说明：
>
> group：在当前的版本保持为None，不要进行修改
>
> target: 这个线程要干的活（函数）
>
> name: 线程名
>
> args： 上面target参数的入参()，tuple类型,对应taget参数中的可变参数
>
> kwargs：上面target参数的入参，dict类型，对应taget参数中的关键字参数

```python
import threading


def my_fun():
    print("hello world")

threading.Thread(target=my_fun).start()
threading.Thread(target=my_fun).start()
```

## 6.2 线程安全问题

**线程安全性问题的三要素：**

- 多线程环境下
- 共享变量
- 并发对共享变量进行修改

```python
import threading


class MyThread(threading.Thread):

    index = 0

    def run(self):
        for i in range(1000000):
            MyThread.index += 1


my_thread1 = MyThread()
my_thread2 = MyThread()
my_thread3 = MyThread()

my_thread1.start()
my_thread2.start()
my_thread3.start()

my_thread1.join()
my_thread2.join()
my_thread3.join()

print(MyThread.index)
# 1987579(每次都不一样)
```

解决多线程的问题，就需要使用**锁**，简单的案例

```python
import threading


class MyThread(threading.Thread):

    index = 0

    # 创建一把锁
    lock = threading.Lock()

    def run(self):
        with MyThread.lock:
            for i in range(1000000):
                MyThread.index += 1


my_thread1 = MyThread()
my_thread2 = MyThread()
my_thread3 = MyThread()

my_thread1.start()
my_thread2.start()
my_thread3.start()

my_thread1.join()
my_thread2.join()
my_thread3.join()

print(MyThread.index)
# 3000000
```

## 6.3 多进程

```python
import multiprocessing
import time


def print_name(thread_name):
    count = 0
    while count < 5:
        time.sleep(1)
        count += 1
        print(thread_name)


if __name__ == "__main__":
    process = multiprocessing.Process(target=print_name, args=("多进程",))
    process.start()
    process.join()
```

