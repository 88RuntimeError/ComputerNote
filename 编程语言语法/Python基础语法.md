# 一、高级变量

在Python中，所有**非数字型变量**都支持以下几个特点

- 1.都是一个**序列** `sequence`，也可以理解为**容器**
- 2.取值方式 `[ ]`
- 3.遍历 `for in`
- 4.计算长度、最大/最小值、比较、删除
- 5.链接 `+`和重复`*`
- 6.切片

## 1. 列表

### (1) 定义

```python
#有值的列表
lis = [1,2,3,4,5]
#空列表
lis = []
```

### (2) 列表提供的方法

```python
'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort'
```

#### 1. append

**描述：append() 方法用于在列表末尾添加新的对象。**

```python
'''
list.append(obj)
	obj -- 添加到列表末尾的对象。
'''

lis = [1,2,3,4,5]
lis.append(6)
#result
lis = [1,2,3,4,5,6]
```

#### 2. clear

**描述：clear()方法用于清空列表**

```python
'''
list.clear()
	无参函数
'''

lis = [1,2,3,4,5] 
lis.clear()
#result
lis = []
```

#### 3. copy

**描述：copy()方法用于实现列表的浅拷贝**

```python
'''
list.copy()
	无参函数
'''

lis = [1,2,3,4,5]
lis2 = lis.copy()  
#result
lis2 = [1,2,3,4,5]
```

#### 4. count

**描述：count() 方法用于统计某个元素在列表中出现的次数。**

```python
'''
list.count(obj)
	obj -- 列表中统计的对象。
'''

lis = [1,1,1,2,3,1,5]
num = lis.count(1)
#result
num = 4
```

#### 5. extend

**描述：extend() 函数用于在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）。**

```python
'''
list.extend(seq)
	seq -- 元素列表。
'''

lis1 = [1,2,3]
lis2 = [4,5,6]
lis1.extend(lis2)
#result
lis1 = [1,2,3,4,5,6]
```

#### 6. index

**描述：index() 函数用于从列表中找出某个值第一个匹配项的索引位置。**

```python
'''
list.index(obj, [start], [end])
	obj-- 查找的对象。
	start-- 可选，查找的起始位置。
	end-- 可选，查找的结束位置。
'''

lis = [1,2,3,4,5]
index = lis.index(5)   
#result
index = 4
```

#### 7. insert

**描述：insert() 函数用于将指定对象插入列表的指定位置。**

```python
'''
list.insert(index, obj)
	index -- 对象obj需要插入的索引位置
	obj -- 要插入列表中的对象。
'''

lis = [1,2,3,5]
lis.insert(3,4)
#result
lis = [1, 2, 3, 4, 5]
```

#### 8. pop

**描述：pop() 函数用于移除列表中的一个元素（默认最后一个元素），并且返回该元素的值。**

```python
'''
list.pop([index=-1])
	index -- 可选参数，要移除列表元素的索引值，不能超过列表总长度，默认为 index=-1，删除最后一个列表值。
'''

lis1 = [1,2,3,4,5]
lis2 = [1,2,3,4,5]
lis1.pop()   #默认是删掉最后一个元素
lis2.pop(0)  #也可以删除指定位置元素
#result
lis1 = [1,2,3,4]
lis2 = [2,3,4,5]
```

#### 9. remove

**描述：remove() 函数用于移除列表中某个值的第一个匹配项。**

```python
'''
list.remove(obj)
	obj -- 列表中要移除的对象。
'''

lis = [1,2,3,4,3]
lis.remove(3)
#result
lis = [1, 2, 4, 3]
```

#### 10. reverse

**描述：reverse() 函数用于反向列表中元素。**

```python
'''
list.reverse()
	无参函数
'''

lis = [1,2,3,4,5]
lis.reverse()
#result
lis = [5,4,3,2,1]
```

#### 11. sort

**sort() 函数用于对原列表进行排序，如果指定参数，则使用比较函数指定的比较函数。**

```python
'''
list.sort(cmp=None, key=None, reverse=False)
	cmp -- 可选参数, 如果指定了该参数会使用该参数的方法进行排序
	key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序
	reverse -- 排序规则，reverse = True 降序， reverse = False 升序（默认）
'''
lis1 = [1,5,3,4,2]
lis2 = [1,5,3,4,2]
lis1.sort()
lis2.sort(reverse=True)
#result
lis1 = [1,2,3,4,5]
lis2 = [5,4,3,2,1]
```

## 2. 元组

### (1) 定义

```python
#有值的元组
tup = ('张三',18,175)
#空元组
tup = ()
#只含一个元素的元组
tup = (1,) #要跟一个逗号，否则认为是int型(内含的数据类型)
```

### (2) 元组提供的方法

```python
'count', 'index'
```

#### 1. count

**描述：count() 方法用于统计某个元素在元组中出现的次数。**

```python
'''
tuple.count(obj)
	obj -- 元组中统计的对象。
'''

tup = ('张三',18,175)
num = tup.count('张三')
#result
num = 1
```

#### 2. index

**描述：index() 函数用于从元组中找出某个值第一个匹配项的索引位置。**

```python
'''
tuple.index(obj, [start], [end])
	obj-- 查找的对象。
	start-- 可选，查找的起始位置。
	end-- 可选，查找的结束位置。
'''

tup = ('张三',18,175)
num = tup.index('张三')
#result
num = 0
```

## 3. 字典

### (1) 定义

```python
xiaoming = {"name":"小明",
            "age":18,
           	"sex":"male",
           	}
#增加字典值               
xiaoming["height"] = 175
xiaoming["weight"] = 75.5

#result
{'name': '小明', 'age': 18, 'sex': 'male', 'height': 175, 'weight': 75.5}
```

### (2) 字典提供的方法

```python
'clear', 'copy', 'fromkeys', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values'
```

#### 1. clear



## 4. 字符串

## 5. 公共方法

### (1) 内置函数

|      函数      |                 描述                  |
| :------------: | :-----------------------------------: |
| **len (item)** |          计算容器中元素个数           |
| **del (item)** |         删除变量（两种方式）          |
| **max (item)** | 返回容器中元素最大值（字典按key比较） |
| **min (item)** | 返回容器中元素最小值（字典按key比较） |

**字符串比较规则："0"<"A"<"a"**

### (2) 切片

```python
lis = [1,2,3,4,5,6,7,8,9]
lis1 = lis[0:6]
lis2 = lis[0:6:2]
lis3 = lis[::3]
lis4 = lis[::-3]
lis5 = lis[6::-2]

#result
[1, 2, 3, 4, 5, 6]
[1, 3, 5]   
[1, 4, 7]   
[9, 6, 3]   
[7, 5, 3, 1]
```

### (3) 完整的 for 循环

```python
for 变量 in 集合:
    循环体代码
else:
    没有通过break退出循环，循环结束后，会执行的代码
    若通过break退出循环，则不会执行该代码
```



# 二、变量进阶

## 1. 变量的引用

- **变量**和**数据**都是保存在内存中的
- 在Python中**函数**的**参数传递**以及**返回值**都是靠**引用**传递的

在Python中

- **变量**和**数据**是分开存储的

- **数据**保存在内存中的一个位置

- **变量**中保存着数据在内存中的地址

- **变量**中**记录数据的地址**，就叫做**引用**

- 使用`id()`函数可以查看变量中保存数据所在的**内存地址**

  ```python
  a = 1
  b = 2
  c = 1
  #result
  id(a) = 1743905947888
  id(b) = 1743905947920
  id(c) = 1743905947888
  
  a = 2
  #result
  id(a) = 1743905947920
  id(b) = 1743905947920
  id(c) = 1743905947888
  ```

## 2. 可变和不可变类型

- 不可变类型，内存中的数据不允许被修改：

  - 数字类型：`int`,`bool`,`float`,`complex`,`long(2,x)`

  - 字符串：`str`
  - 元组：`tuple`

- 可变类型，内存中的数据可以被修改
  - 列表：`list`
  - 字典：`dict`

## 3. 局部变量和全局变量

**局部变量：**是在 **函数内部** 定义的变量，只能在函数内部使用

**全局变量：**是在 **函数外部定义** 的变量（没有定义在某一个函数内），**有所函数** 都可以使用这个变量

### (1) 局部变量

- **局部变量** 是在 **函数内部** 定义的变量，只能在函数内部使用
- 函数执行结束后，**函数内部的局部变量会被系统回收**
- 不同的函数，可以定义相同的名字的局部变量，相互之间不会产生影响

**局部变量的作用**

- 在函数内部使用，**临时** 保存 **函数内部需要使用的数据**

**局部变量的生命周期**

- 所谓生命周期，就是变量从被创建到被系统回收的过程
- 局部变量在函数执行时才会被创建
- 函数执行结束后局部变量会被系统回收
- 局部变量在生命周期内，可以用来存储函数内部临时使用到的数据

### (2) 全局变量

- **全局变量** 是在 **函数外部** 定义的变量，所有函数内部都可以使用这个变量

- 注意：函数执行，需要处理变量时，会：

  1. 首先查找函数内部是否存在指定名称的局部变量，如果有，直接使用

  2. 如果没有，查找函数外部是否存在指定名称的全局变量，如果有，直接使用

  3. 如果还没有找到，程序报错

     

- 在函数内部，可以 **通过全局变量的引用获取对应的数据**

- 但是，**不允许直接修改全局变量的引用** —— 使用赋值语句修改全局变量的值

  ```python
  num = 1
  print("全局变量num的地址 = %d" % id(num))
  def demo1():
      num = 99
      print("demo1.num = %d" % num)
      print("demo1.num的地址 = %d" % id(num))
  
  def demo2():
      print("demo2.num = %d" % num)
      print("demo2.num的地址 = %d" % id(num))
  
  demo1()
  demo2()
  
  #result
  全局变量num的地址 = 2974041243888
  demo1.num = 99
  demo1.num的地址 = 2974041247024
  demo2.num = 1
  demo2.num的地址 = 2974041243888
  #可以看出，demo1只是修改了局部变量num，并没有对全局变量num进行修改
  ```

- 在**函数内部修改**全局变量的值，需要使用 `global` 进行声明

  ```python
  num = 1
  print("全局变量num的地址 = %d" % id(num))
  def demo1():
      global num 
      num = 99
      print("demo1.num = %d" % num)
      print("demo1.num的地址 = %d" % id(num))
  
  def demo2():
      print("demo2.num = %d" % num)
      print("demo2.num的地址 = %d" % id(num))
  
  demo1()
  demo2()
  
  #result
  全局变量num的地址 = 1354694721776
  demo1.num = 99
  demo1.num的地址 = 1354694724912
  demo2.num = 99
  demo2.num的地址 = 1354694724912
  #可以看出，demo1中添加global关键字后，全局变量num的值就被修改成功了
  ```

- 全局变量命名建议
  - 为了避免局部变量和全局变量出现混淆，在定义全局变量时，有些公司会有一些开发要求，例如：
  - 全局变量名前应该增加 `g_` 或者 `gl_` 的前缀





# 三、面向对象

## 1. 面向过程和面向对象的基本概念

### (1) 面向过程 —— (怎么做?)

1. 把完成某一个需求的 `所有步骤` `从头到尾` 逐步实现
2. 根据开发需求，将某些 **功能独立** 的代码 **封装** 成一个又一个 **函数**
3. 最后完成代码，就是顺序地调用 **不同的函数**

**特点**

1. 注重 **步骤与过程**，不注重职责分工
2. 如果需求复杂，代码会变得很复杂
3. **开发复杂项目，没有固定的套路，开发难度很大**

![1650119460(1)](D:\Desktop\1650119460(1).jpg)

### (2) 面向对象 —— (谁来做?)

> 相比较函数，**面向对象** 是 **更大** 的 **封装**，根据 **职责** 在 **一个对象中封装多个方法**

1. 在完成某一个需求前，首先确定 **职责——要做的事情(方法)**
2. 根据 **职责** 确定不同的 **对象**，在 **对象** 内部封装不同的 **方法(多个)**
3. 最后完成的代码，就是顺序地让 **不同对象** 调用 **不同的方法**

**特点**

1. 注重 **对象和职责**，不同的对象承担不同的职责
2. 更加适合应对复杂的需求变化，**是专门应对复杂项目开发，提供的固定套路**
3. **需要在面向过程基础上，再学习一些面向对象的语法**

## 2. 类和对象

**类** 和 **对象** 是 **面向对象编程的** 两个 **核心概念**

### (1) 类

- **类** 是对一群具有 **相同特征** 或者 **行为** 的事物的一个统称，是抽象的，**不能直接使用**
  - **特征** 被称为 **属性**
  - **行为** 被称为 **方法**

- **类** 就相当于制造飞机时的**图纸**，是一个**模板**，是**负责创建对象的**

### (2) 对象

- **对象** 是由 **类创建出来的一个具体存在**，可以直接使用
- 由 **哪一个类** 创建出来的 **对象**，就拥有在 **哪一个类** 中定义的 **属性** 和 **方法**
- **对象** 就相当于用 **图纸  制造** 的飞机

### (3) 类和对象的关系

- 类是模板，对象是根据类这个模版创建出来的，应该**先有类，再有对象**
- 类只有一个，而对象可以有很多个
  - **不同的对象 **之间 **属性** 可能会各不相同

- **类** 中定义了什么属性和方法，**对象** 中就有什么属性和方法，不可能多，也不可能少

### (4) 类的设计

在使用面向对象开发之前，应该首先分析需求，确定一下，程序中需要包含哪些类

在程序开发中，要设计一个类，通常需要满足以下三个要素：

1. **类名：**这类事物的名字，**满足大驼峰命名法**
2. **属性：**这类事物具有什么样的特征
3. **方法：**这类事物具有什么样的行为

**大驼峰命名法**

`CapWords`

1. 每一个单词的首字母大写
2. 单词与单词之间没有下划线

### (5) dir内置函数

使用内置函数 `dir` 传入 `标识符/数据` ，可以查看对象内的 **所有属性及方法**

**提示：**`__方法名__` 格式的方法是 `Python` 提供的 **内置方法/属性**

| 序号 |      方法名      | 类型 |                 作用                  |
| :--: | :--------------: | :--: | :-----------------------------------: |
|  1   | **\_\_new\_\_**  | 方法 |       创建对象时，会被自动调用        |
|  2   | **\_\_init\_\_** | 方法 |     对象被初始化时，会被自动调用      |
|  3   | **\_\_del\_\_**  | 方法 |   对象被从内存销毁时，会被自动调用    |
|  4   | **\_\_str\_\_**  | 方法 | 返回对象的描述信息，print函数输出使用 |

## 3. 定义简单的类

### (1) 定义只包含方法的类

- 在 `Python` 中要定义一个只包含方法的类，语法格式如下：

```python
class 类名:
    def 方法一(self,参数列表):
        pass
    def 方法二(self,参数列表):
        pass
```

- **方法** 的定义格式和之前学过的 **函数** 几乎一样
- 区别在于第一个参数必须是 `self`
- 类名的命名规则要符合大驼峰命名法

### (2)创建对象

- 当一个类定义完成之后，要使用这个类来创建对象，语法格式如下：

```python
对象变量 = 类名()
```

### (3) 第一个面向对象程序

```python
#创建猫类
class Cat:
    def eat(self):
        #哪一个对象调用的方法，self就是哪个对象的引用
        print("小猫要吃鱼")
    def drink(self):
        print("小猫要喝水")

#创建猫对象
tom = Cat()
tom.eat()
tom.drink()

#result
小猫要吃鱼
小猫要喝水
```

## 4. 内置方法和属性

### 4.1 \_\_init\_\_方法

- 当使用 `类名()` 创建对象时，会 **自动** 执行以下操作：
  1. 为对象在内存中 **分配空间** —— 创建对象
  2. 为对象的属性 **设置初始值** —— 初始化方法`(init)`

- 这个 **初始化方法** 就是 `__init__`方法，`__init__` 是对象的内置方法，`__init__` 方法是专门用来定义一个类 **具有哪些属性** 的方法

```python
class Cat:
    def __init__(self):
        print("这是一个初始化方法")

tom = Cat()

#result
这是一个初始化方法
```

- `__init__` 方法会在创建对象时被自动调用



- 在开发中，如果希望 **创建对象的同时，就设置对象的属性**，可以对 `__init__` 方法进行 **改造**
  1. 把希望设置的属性值，定义成 `__init__` 方法的参数
  2. 在方法内部使用 `self.属性 = 形参` 接收外部传递的参数
  3. 在创建对象时，使用 `类名(属性1, 属性2 ...)` 调用

```python
class Cat:
    def __init__(self, newname):
        #定义用 Cat 类创建的猫对象都有一个 name 的属性
        self.name = newname

    def eat(self):
        print("%s 爱吃鱼" % self.name)

tom = Cat("Tom")
tom.eat()
lazy_cat = Cat("大懒猫")
lazy_cat.eat()

#result
Tom 爱吃鱼
大懒猫 爱吃鱼
```

### 4.2 内置方法和属性

| 序号 | 方法名          | 类型 | 作用                                          |
| ---- | --------------- | ---- | --------------------------------------------- |
| 01   | **\_\_del\_\_** | 方法 | **对象被从内存中销毁** 前，会被 **自动** 调用 |
| 02   | **\_\_str\_\_** | 方法 | 返回 **对象的描述信息**，print 函数输出使用   |

#### 4.2.1 \_\_del\_\_ 方法

```python
class Cat:
    def __init__(self, newname):
        self.name = newname
        print("%s 被创建了" % self.name)

    def __del__(self):
        print("%s 被销毁了" % self.name)

#tom是一个全局变量，所有代码执行完成之后，系统才会把tom回收
tom = Cat("Tom")
print("-" * 50)

lazy_cat = Cat("大懒猫")
#del可以手动删除指定对象
del lazy_cat
print("*" * 50)
```

#### 4.2.2 \_\_str\_\_ 方法

- 在 `Python` 中，使用 `print` 输出 **对象变量**，默认情况下，会输出这个变量 **引用的对象** 是 **由哪一个类创建的对象**，以及 **在内存中的地址（十六进制表示）**
- 如果在开发中，希望使用 `print` 输出 **对象变量** 时，能够打印 **自定义的内容**，就可以利用 `__str__` 这个内置方法
- 注意 `__str__` 方法必须返回一个字符串

```python
class Cat:
    def __init__(self, newname):
        self.name = newname

    def __del__(self):
        pass

class Cat2:
    def __init__(self, newname):
        self.name = newname

    def __del__(self):
        pass
    
    def __str__(self):
        #__str__必须返回一个字符串
        return "我是小猫[%s]" % self.name


tom = Cat("Tom")
lazy_cat = Cat2("Lazy")
print(tom)
print(lazy_cat)

#result
<__main__.Cat object at 0x0000028067A13BE0>
我是小猫[Lazy]
```

## 5. 封装

1. **封装** 是面向对象编程的一大特点
2. 面向对象编程的 **第一步** —— 将 **属性** 和 **方法** **封装** 到一个抽象的 **类** 中
3. **外界** 使用 **类** 创建 **对象**，然后 **让对象调用方法**
4. **对象方法的细节** 都被 **封装** 在 **类的内部**

### 5.1 封装小案例——小明爱跑步

**需求**

1. **小明** **体重** `75.0 `公斤
2. 小明每次 **跑步** 会减肥 `0.5`公斤
3. 小明每次 **吃东西** 体重增加 `1` 公斤

![image-20220419085309190](C:\Users\1234\AppData\Roaming\Typora\typora-user-images\image-20220419085309190.png)

```python
class Person:
    def __init__(self, name, weight):
        # self.属性 = 形参
        self.name = name
        self.weight = weight

    def __str__(self):
        #__str__必须返回字符串
        return "我的名字叫 %s, 体重是 %.2f 公斤" % (self.name, self.weight)

    def run(self):
        print("我现在的体重是 %.2f" % self.weight)
        self.weight -= 0.5
        print("我跑完步啦, 现在的体重是 %.2f" % self.weight)

    def eat(self):
        print("我现在的体重是 %.2f" % self.weight)
        self.weight += 1
        print("我吃完东西啦, 现在的体重是 %.2f" % self.weight)

xiaoming = Person("小明",75.0)
xiaoming.run()
xiaoming.eat()

#result
我现在的体重是 75.00
我跑完步啦, 现在的体重是 74.50
我现在的体重是 74.50
我吃完东西啦, 现在的体重是 75.50
```

### 5.2 封装调用封装小案例——摆放家具

**需求**

1. **房子(House)** 有 **户型、总面积** 和 **家具名称列表**
   - 新房子没有任何家具
2. **家具(HouseItem)** 有 **名字** 和 **占地面积**，其中
   - **席梦思(bed)** 占地 `4` 平米
   - **衣柜(chest)** 占地 `2` 平米
   - **餐桌(table)** 占地 `1.5` 平米
3. 将以上三件 **家具** **添加** 到 **房子** 中
4. 打印房子时，要求输出：**户型、总面积、剩余面积、家具名称列表**
5. 添加家具时，要先 **判断** 剩余面积是否足够添加

![image-20220419090816839](C:\Users\1234\AppData\Roaming\Typora\typora-user-images\image-20220419090816839.png)

```python
class HouseItem:
    def __init__(self, name, area):
        self.name = name
        self.area = area
    
    def __str__(self):
        return "[%s] 占地 %.2f" % (self.name, self.area)

class House:
    def __init__(self, house_type, area):
        self.house_type = house_type
        self.area = area
        # 剩余面积
        self.free_area = area
        # 家具名称列表
        self.item_list = []
    
    def __str__(self):
        #Python能够自动将一个括号内的代码连接在一起
        return ("户型: %s \n总面积: %.2f[剩余: %.2f]\n家具: %s" 
        % (self.house_type,self.area,self.free_area,self.item_list))

    def add_item(self, item):
        print("要添加 %s" % item)
        #1. 判断家具的面积
        if item.area > self.free_area:
            print("%s 的面积太大了, 无法添加" % item.name)
            return
        #2. 将家具的名称添加到列表中
        self.item_list.append(item.name)
        #3. 计算剩余面积
        self.free_area -= item.area

# 1. 创建家具
bed = HouseItem("席梦思",20)
chest = HouseItem("衣柜",30)
table = HouseItem("餐桌",40)

# 2. 添加家具
my_home = House("两室一厅",60)
my_home.add_item(bed)
my_home.add_item(chest)
my_home.add_item(table)
print(my_home)

#result
要添加 [席梦思] 占地 20.00
要添加 [衣柜] 占地 30.00
要添加 [餐桌] 占地 40.00
餐桌 的面积太大了, 无法添加
户型: 两室一厅
总面积: 60.00[剩余: 10.00]
家具: ['席梦思', '衣柜']
```

### 5.3 封装属性是封装小案例——士兵突击

**需求**

1. **士兵** **许三多** 有一把 **AK47**
2. **士兵** 可以 **开火**
3. **枪** 能够 **发射** 子弹
4. **枪** 装填 **装填子弹——增加子弹数量**

![image-20220419100336783](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220419100336783.png)

- **定义没有初始值的属性**

  在定义属性时，如果 **不知道设置什么初始值**，可以设置为 `None`

  - `None` **关键字** 表示 **什么都没有**
  - 表示一个 **空对象，没有方法和属性，是一个特殊的常量**
  - 可以将 `None` 赋值给任何一个变量
  - 针对 `None` 比较时，建议使用 `is` 判断
  - `is` 用于判断两个变量 **引用对象是否为同一个**
  - `==` 用于判断 **引用变量的值** 是否相等

```python
class Gun:
    def __init__(self, model):
        # 1.枪的型号
        self.model = model
        # 2.子弹的初始数量
        self.bullet_count = 0

    def add_bullet(self, count):
        self.bullet_count += count

    def shoot(self):
        # 1.判断子弹数量
        if self.bullet_count <= 0:
            print("[%s] 没有子弹了" % self.model)
            return
        # 2.发射子弹 -1
        self.bullet_count -= 1
        # 3.提升发射信息
        print("[%s] 突突突, 剩余[%d]颗子弹" % (self.model, self.bullet_count))


class Solider:
    def __init__(self, name):
        self.name = name
        self.gun = None

    def fire(self):
        # 1.判断士兵是否有枪
        if self.gun is None:
            print("%s 还没有枪" % self.name)
            return
        # 2.判断枪中是否有子弹
        print("%s 高喊：冲啊！" % self.name)
        if self.gun.bullet_count <= 0:
            self.gun.add_bullet(50)
        # 3.让枪发射子弹
        self.gun.shoot()

ak47 = Gun("AK47")
xusanduo = Solider("许三多")
xusanduo.gun = ak47
xusanduo.fire()

#result
许三多 高喊：冲啊！
[AK47] 突突突, 剩余[49]颗子弹
```

### 5.4 私有属性和私有方法

**定义方式**

- 在 **定义属性或方法时**，在 **属性名或者方法名前** 增加 **两个下划线**，定义的就是 **私有属性或方法**

  ![image-20220419103657230](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220419103657230.png)

- 私有属性不能在外界直接调用
- 私有熟悉可以通过共有方法间接访问

```python
class Women:
    def __init__(self, name):
        self.name = name
        self.__age = 18

    def secret(self):
        print("%s 的年龄是 %d" % (self.name, self.__age))

xiaofang = Women("小芳")
print(xiaofang.secret())
print(xiaofang.__age)

#result
小芳 的年龄是 18
None
Traceback (most recent call last):
  File "D:\MyCode\MyTest\test.py", line 11, in <module>
    print(xiaofang.__age)
AttributeError: 'Women' object has no attribute '__age'

Process finished with exit code 1
```

- 私有方法不能在外界直接调用

```python
class Women:
    def __init__(self, name):
        self.name = name
        self.__age = 18

    def __secret(self):
        print("%s 的年龄是 %d" % (self.name, self.__age))

xiaofang = Women("小芳")
print(xiaofang.secret())

#result
Traceback (most recent call last):
  File "D:\MyCode\MyTest\test.py", line 10, in <module>
    print(xiaofang.secret())
AttributeError: 'Women' object has no attribute 'secret'
```

### 5.5 伪私有属性和私有方法

在 `Python` 中，没有真正意义上的私有

- 在给 **属性、方法** 命名时，实际是对 **名称** 做了一些特殊处理，使得外界无法访问到
- **处理方式：** 在 **名称** 前面加上 `_类名` => `_类名__名称`
- 在日常开发中，不要使用这种方式，访问对象的私有属性或私有方法

```python
class Women:
    def __init__(self, name):
        self.name = name
        self.__age = 18

    def __secret(self):
        print("%s 的年龄是 %d" % (self.name, self.__age))

xiaofang = Women("小芳")
# 伪私有访问方法（可以正常访问，不推荐这样做）
print(xiaofang._Women__age)
print(xiaofang._Women__secret())
# 正常外界调用（会报错）
print(xiaofang.__age)
print(xiaofang.secret())

#result
18
小芳 的年龄是 18
None
Traceback (most recent call last):
  File "D:\MyCode\MyTest\test.py", line 12, in <module>
    print(xiaofang.__age)
AttributeError: 'Women' object has no attribute '__age'

Process finished with exit code 1
```

## 6. 继承

