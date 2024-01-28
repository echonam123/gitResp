[TOC]

# 海龟绘图

图形化程序设计

```python
import turtle # 引入海龟绘图模块

p=turtle.Pen # 画笔对象
p.speed(10) # 改变速度
p.showturtle() #显示画笔
p.penup() #把笔抬起
p.goto(x,y) #把笔移到x,y坐标
p.color("red") #把画笔颜色改成红色
p.width(10) # 把画笔变粗
p.write("something") #写字符串
p.left(90) #把画笔旋转90度
p.forward(100) # 画直线，前进100像素
p.circle(r) # 画圆

turtle.done() #程序结束后不关闭程序运行窗口
```



# 错误和异常捕获

## 异常捕获

- try and except

```python
try:
    n1=int(input('请输入一个整数:'))
    n2=int(input('请输入另一个整数'))
    result=n1/n2
except ZeroDivisionError:
    print('对不起，除数不允许为0')
except ValueError: 
    print('只能输入数字串')
except BaseException:
    print('出错')
except:
    print("发生未知错误，请重新执行程序")
else print('结果为',result) # 不发生错误时
finally print('程序结束') # 无论错误如何都会执行
```

- assert断言

  assert 表达式

  .........

  若表达式为false则触发AssertionError机制，程序结束，不往下运行



## 异常类型

1. ==语法异常:SyntaxError==

   - 无效语法invalid syntax

   - 无效字符invalid character in identifier(一般是用中文字符造成的)

   - 字符串行尾错误EOL while scanning string literal(有可能因为引号没有闭合或者没有使用三引号（''')来标识跨行字符串比如:)

     > exercise='1234，
     >
     > 1234，
     >
     > 1234‘
     >
     > 应该改成：
     >
     > exercise='''1234，
     >
     > 1234，
     >
     > 1234'''

   - 语法不完整unexpected EOF while parsing(一般是'()'没有成对出现)

2. ==变量名错误NameError==

   - 字符串变量没有加引号(如open文件的时候没有给文件打双引号)
   - 变量超出作用域
   - 关键字拼写错误

3. ==传入值错误ValueError==

   - 无效参数invalid literal(比如int()括号里可以传入字符串，数字，但传入浮点型的字符串就会报错eg:'66.6')

   -  传入参数过多too many values to unpack(参数个数不同)

   - 数学域错误math domain error(不符合数学原则)

     > 比如负数-4求平方根，但是因为负数没有平方根，可以引入cmath模块，得到一个负数
     >
     > import cmath
     >
     > x=-4
     >
     > print(cmath.sqrt(x))

   - 数据维度不符operands could not be broadcast together with shapes

4. ==缩进错误IndentationError==

5. ==除数为0错误ZeroDivisionError==

   (取余%0也不行，另外若是浮点数计算除数为接近0的数也不行，因为浮点数计算会有一点精度损失)

6. ==索引错误IndexError==

   - 索引越界
   - 索引必须是整数或者切片

7. ==未找到指定文件FileNotFoundError==

   > 确定程序当前工作目录方法:
   >
   > import os
   >
   > print(os.getcwd( ))

8. ==属性错误AttributeError==

   - 属性名称错误或者不存在
   - 模块属性使用错误

9. ==引用未定义的局部变量UnboundLocalError==

10. ==未找到对应键值KeyError==

    - 解决方法:用get若是键不存在就返回None

      ​	或者使用setdefault和get一样不存在会返回none但是不一样的是会改变字典，在字典中加入查找的key

      ​	或者使用collections模块中的defaultdict()方法

      ​	eg:

      ```python
      # defaultdict()
      
      from collections import defaultdict
      
      role_dict=defaultdict(int) # 提供默认值int则默认为0
      
      role_dict={'name':'慕容云海'}
      print(role_dict['颜值'])
      print(role_dict)
      
      结果是:{'name':'慕容云海','颜值':0}
      ```

11. ==无效类型typeError==

12. ==数值运算超出最大限制OverError==

    > python中整数可以是无限大的，但是浮点数可以有限制
    >
    > ![image-20240126175743890](https://typora-011.oss-cn-guangzhou.aliyuncs.com/image-20240126175743890.png)

- 类型转化解决方法：在将int转成浮点型的时候要判断，若是超过float承受的最大限制则认为是无穷大

  ```pythonimport sys
  if result_int>sys.float_info.max:
      result_float=float('info')
  ```

- e的n次幂过大解决方法:先找到e的最大次幂,若现在的幂次大于最大幂次，则认为是无穷大

  ```python
  import sys
  import math
  max_e=math.log(sys.float_info.max)
  if euler<max_e:
      result=math.exp(euler)
  else:result=float('info')
  ```





# 数据类型

## 整数

python3可以存储无限大的整数

## 浮点数

小数点表示或者科学计数法

## 布尔

True or False

## 复数

==a=1+2j==    is equal to  ==a=complex(1,2)==



 # 基础语法

## 注释

1. 单行注释：每行注释前加上'#'即可
2. 多行注释：使用三个连续单引号或者双引号（'''或者""")可以注释之间的内容

## 连接符

python解释器中回车直接运行，但是为了可读性更强，将比较长的代码分多行书写，会使用\连接符

## 对象

python里面一切皆是对象(包括None)，每个对象由标识(id)，类型，值组成



# 数据结构

## 字符串

1. 可变字符串的创建

   字符串是不可变的，replace是创建新的字符串修改的，创建可变字符串的典型例子如下：

```python
import io # 插进模块
s='hello world' 
sio=io.StringIO(s) # 创建可变字符串
sio.seek(1) # 找到索引1
sio.write('appy') # 修改值
print(sio.getvalue()) # 输出修改后的
```

2. 格式化format

3. 切片

   s[start':''end':'step]

## 列表

1. 创建列表

(1)直接创建

(2)list，range创建

(3)推导式

2. 列表的增加和删除

   append,del,pop,clear,'+'运算符,extend,'*'扩展，remove

3. 查找index

4. 返回列表长度len

5. 返回元素出现次数count

6. 列表遍历for i in listobj

7. 排序：

   (1)修改原列表，sort()是升序,sort(reverse=true)是降序

   (2)创建新列表,sorted()

   (3)逆序也可以使用迭代器reversed

8. 最大最小值，求和

   max,min,sum

9. in成员判断



## 字典

1. 创建字典

   (1)直接创建

   (2)dict创建,元组也可以作为一个键对

   (3)生成器推导式

   (4)fromkeys创建空字典

   ```python
   a=dict.fromkeys(['name','age','address'])
   print(a)
   ```

2. get若读取字典中没有的键则返回defalut值，一般默认为None

3. 读取所有键keys(),

4. 读取所有值values(),

5. update更新字典

6. pop删除键对

7. 散列表底层原理

   

## 元组

1. 创建元组：

   (1)直接创建

   (2)tuple

   (3)zip

   (4)生成器推导式

2. 元组是不可变序列

   

## 集合

1. 无序,不重复，元素不能为列表

2. 创建集合

   (1)‘{}’直接创建

   (2)set()

3. 并集，交集，差集，并集-交集

4. 判断是否有相同元素

   .isdisjoint()

   没有则返回true，有则false

5. 判断a是否为b的子集

   a.issubset(b)

   是则返回true




# 特殊函数

## lambda

匿名函数，可以实现定义和实现在一行中完成（简洁性）

lambda x,y....[参数列表]:[表达式]

```python
add=lambda x,y:x+y
print(add(1,2))
```

结果为3

## eval

将字符串str当成有效表达式来求值，并返回计算结果

```python
a=10
b=20
c=eval('a+b')
print(c)
```

结果为30

## filter

过滤器

```python
numbers=[1,2,3,4,5,6,7,8,9]
result=list(filter(lambda x:x%2==0,numbers))
print(result)
```

结果是[2, 4, 6, 8]

## map

将可迭代对象统一用函数对象进行处理

map(函数对象，可迭代对象)

```python
def doubler(n):
    return n*2
print(list(map(doubler,[1,3,5,7,9])))
```

结果是[2, 6, 10, 14, 18]



# 类

## 类的定义和创建

类就像饼干的模具一样，可以创建出无数个相似的饼干

类的名字遵从‘驼峰原则’

```python
class Car:  #类的创建
    wheels=4
    def __init__(self,type):
        self.type=type
        
if __name__=="__main__":
    car1=Car("奥迪")    #实例
    car2=Car("宝马")
```

## 属性与方法

1. 属性分为类属性和实例属性，类属性是所有实例所共有的

2. 方法分为类方法和实例方法

在定义类方法时需要在上方写上@classmethod，例如：

```python
class Car:  #类的创建
    wheels=4
    def __init__(self,type):
        self.type=type
        
    @classmethod
    def drive(cls):
        print("driving")
```

## 三大特点

### 封装

1. 隐藏对象中一些不希望外部所访问到的属性或方法，即为了保证安全

2. 私有属性及私有方法的定义：在名字前方加上两个下划线(__)即可，私有属性和私有方法都是只能在类内部使用

3. 类的属性方法：可以通过装饰器(property，setter)将一个方法，转换为对象的属性

   例如：

   ```python
   class Car:  #类的创建
       wheels=4
       def __init__(self,type,age):
           self.type=type
           self.__age=age  #私有属性
       @classmethod
       def drive(cls):
           print("driving")
   
       @property
       def age(self):
           return self.__age
   
       @age.setter
       def age(self,age):
           self.__age=age
   
   
   if __name__=="__main__":
       car1=Car("奥迪",1)    #实例
       car2=Car("宝马",2)
       Car.drive() #类方法
       print(car1.age)
       car1.age=3
       print(car1.age)
   ```

### 继承

Python 支持类的单继承和多继承

- 实现继承的类称为子类，被继承的类称为父类（也可称为基类、超类）
- 一般类默认继承object父类

例子：

```
class Father:	#父亲函数
    xing=('林')
    def __init__(self):
        pass

class Son(Father):	#继承函数
    def __init__(self,name,age):
        self.name=name
        self.age=age

if __name__ == '__main__':
    son1=Son('林彪',30)
    print(son1.name,son1.xing,son1.age)
    print(Son.xing)
```

结果是

林彪 林 30
林

### 多态

同一种行为对不同的子类[对象]有不同的行为表现

例子：

```python
class Animal:	
    def __init__(self):
        pass
    def speak(self):
        print("动物叫了一声")
class Dog(Animal):
    type='dog'
    def __init__(self,name):
        self.name=name
    def speak(self):
        print("汪汪汪")
class Cat(Animal):
    type='cat'
    def __init__(self,name):
        self.name=name
    def speak(self):
        print("喵喵喵")

if __name__=='__main__':
    dog1=Dog('旺财')
    dog1.speak()
    cat1=Cat("小喵")
    cat1.speak()
```

都是speak但是

cat1.speak()结果是'喵喵喵'

dog1.speak()结果是'汪汪汪'





