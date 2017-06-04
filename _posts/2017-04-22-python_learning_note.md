---
layout: post
title: python学习笔记
date: 2017-04-22 11:15:06 
tag: python
---

注：本文档不再更新，比较python官方文档和'廖雪峰'老师的教程，发现有些差别，想脱离廖老师教程，参照官方文档来从新编写。

### 目录
* [Python安装](#How_to setup_Python)
* [函数式编程](#Functional Programming)
* [高级特性](#Advanced Features)
* [面向对象编程](#Object_Oriented_Programming)
## <a name="How_to_setup_Python"></a> Python 的安装

### 安装步骤：
* 1.从Python官网选择对应版本的64位or32位安装包。

* 2.安装Python，注意在安装时，勾选Add Python 3.5 to PATH.

* 3.打开命令提示符窗口，输入python后，可查看python版本等相关信息，若没有表示安装失败。
```
    C:\Users\ljh>python
```
  输入后，看到>>>进入python互交式环境，可输入python代码，回车后可立刻得到执行结果，输入exit()退出Python环境。


## Python解释器

### 常见的几种解释器
* 1.CPython:在命令行下运行python后，启动的就是CPython解释器。

* 2.IPython:IPython是基于CPython之上的一个互交解释器，CPython用>>>作提示符，IPython用In[序号]:作提示符。

* 3.PyPy:PyPy采用JIT技术，对python代码进行动态编译，所以来提高python执行效率。

* 4.Jython:Jython是运行在java平台的Python解释器，可以直接包Python代码编译成Java字节码执行。

* 5.IronPython:IronPython和Jython类似，IronPython是运行在微软.Net平台的Python解释器，可以把代码直接编译为.Net字节码。


## Python书写格式

* 1.#开头的语句为注释。
* 2.Python使用4个空格缩进来组织代码块，以：结尾时，缩进的语句为代码块。

example:
```python
    #print absolute value of an integer:
	a=100
	if a>=0:
	    print(a)
	else:
	    print(-a)
```



## 数据类型
  整数（0,1，2,-10），浮点数（0.1，-20,21），字符串('abc',"abc",'I\'m \"OK\"!'),布尔值(True,False),空值(None).
  <br>
  一些例子：
  ```python
  	 a='ABC'
	 b=a
	 a='XYZ'
	 print(b)  #output:ABC


	 >>>10/3   #output:3.33333333333
	 >>>9/3    #output:3.0
	 >>>10//3  #output:3
	 >>>10%3   #output:1
  ```


## 字符编码

### 编码演变
```
ASCII编码(1字节）->中文编码GB2312       
                ├>日文编码Shift-JIS            ->  Unicode（两字节）        ->  utf-8(可变字节)
		├韩文编码Euc-kr         
		└>...                 
```
### 三种编码格式比较
```
字符         |ASCII             |Unicode                     |utf-8
----------- |----------------- |----------------------------|---------------------------
A           |01000001          |00000000 01000001           |01000001          
中          |x                 |01001110 00101101           |11100100 10111000 10101101  

```
### 字符串
字符串以Unicode编码，即python支持多语言
```python
>>>print('包含中文的str')   #output:包含中文的str
```

单字符 -> 整数编码 ord()
<br>
整数编码 -> 字符  chr()

```python
>>>ord('A')   #output:65
>>>ord('中')  #output:20013
>>>chr(66)    #output:B
>>>chr(25991) #output:文

#十六进制表示str
>>> '\u4e2d\u6587'  #output:中文
```

python的字符串类型在内存中以Unicode表示，在保存到文件中或者网络传送时，str转成字节为单位的bytes.
<br>
bytes数据类型用前缀b+单(双)引号表示：
```python
x=b'ABC'
```

'ABC'为字符串  b’ABC'bytes
<br>
str转bytes  encode()
<br>
bytes转str  decode()
```python
>>>'ABC'.encode('ascii')          #output:b'ABC'
>>>'中文'.encode('utf-8')         #output:b'\xe4\xb8\xad\xe6\x96\x87'
>>>'中文'.encode('ascii')         #putput: Traceback...
>>>b'ABC'.decode('ascii')         #putput:’ABC'
>>>b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')   #putput:'中文'
```

str字符数或者字节数 len()
```python
>>>len('ABC')         #output:3
>>>len(b'ABC')        #output:3
>>>len('中文')         #output:2
>>>len(b'\xe4\xb8\xad\xe6\x96\x87') #output:6
```

### Python源码编码问题
<br>
保存源码时，指定保存为utf-8编码，通常在文件开头写下这两行：
```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-
```
第一行表示Linuex/OS X系统，这是一个python可执行程序，Windows系统会忽略这个注释。
<br>
第二行是为了告诉Python解释器，按utf-8编码读取源代码。


### 格式化
```python
>>>'Hello,%s' % 'world'    #output:'Hello,world'
>>>'Hi,%s,you have $%d.' %('Michael',1000000)  #output:'Hi,Michael,you have $100000'
```

### 常用占位符
```
%d |整数
%f |浮点数
%s |字符串
%x |十六进制整数
```
格式化整数和浮点数还可以指定是否补0和整数与小数的位数
```python
>>>'%2d-%02d' %(3,1)         #output:'  3-01'
>>>'%.2f' % 3.1415926        #output:'3.14'
>>>growth rate:%d %%' %7     #%%表示一个%,output:'growth rate:7 %'
```

## list 和tuple

### list
Python内置数据类型，list是一种有序集合，可随时添加和删除元素。
```python
>>>classmates=['Michael','Bob','Tracy']
>>>classmates     #output:['Michael','Bob','Tracy']
```
用len()可以获得list元素个数：
```python
>>>len(classmates)     #output:3
```
用索引来访问list对应位置的元素，第一个索引值从0开始,索引超出范围，会返回IndexError.
```python
>>>classmates[0]       #output:'Michael'
>>>classmate[1]        #output:'Bob'
>>>classmates[2]       #output:'Tracy'
>>>classmates[3]       #output:Traceback...(IndexError)
```
索引为负数idx,表示获取倒数第|idx|个元素。
```python
classmates[-1]     #output:'Tracy'
classmates[-2]     #output:'Bob'
```
往list中插入元素，插入到list尾用list.append(),插入到指定位置，用list.insert()
```python
>>>classmates.append('Adam')
>>>classmates     #output:['Michael','Bob','Tracy','Adam']
>>>classmates.insert(1,'Jack')   #插入Jack到索引1的位置
>>>classmates       #output:['Michael','Jack','Bob','Tracy','Adam']
```
删除list中元素用list.pop()
```python
>>>classmates.pop()       #pop()默认删除最后一个元素
>>>classmates             #output:['Michael','Jack','Bob','Tracy']
>>>classmates.pop(1)      #删除指定索引1位置的元素
>>>classmates             #output:['Michael','Bob','Tracy']
```
替换指定索引元素，直接给指定元素赋值
```python
>>>classmates[1]='Sarah'
>>>classmates            #output:['Michael','Sarah','Tracy']
```
list中的元素的数据类型可以是不同的
```python
>>>L=['Apple',123,True,['python','java','c#']]
>>>p=['asp','php']
>>>s=['a','b',p]          #仅仅作演示作用，然并卵
```
list中没有任何元素，就是一个空list，其长度为0

### tuple
tuple元组，初始化后不能修改，如
```python
>>>classmates=('Michael','Bob','Tracy')
>>>istuple=(1,)     #当tuple只有一个元素时，其元素后要跟一个","来消除歧义
>>>istuple          #output:(1,)
>>>isint=(1)
>>>isint            #output:1
```
可变tuple
```python
>>>t=('a','b',['A','B'])
>>>t[2][0]='X'
>>>t[2][1]='Y'
>>>t              #output:('a','b',['X','Y'])
```
```
┏━━━━━┓          ┏━━━━━┓━━━━━┓━━━━━┓
┃  t  ┃ -------->┃  0  ┃  1  ┃  2  ┃
┗━━━━━┛          ┗━━━━━┛━━━━━┛━━━━━┛    
                    ↓      ↓      ↓ 
                   'a'    'b'   ┏━━━━━┓━━━━━┓
                                ┃  0  ┃  1  ┃
                                ┗━━━━━┛━━━━━┛
                                   ↓      ↓ 
                                  'A'    'B'
                                   ↓      ↓
                                  'X'    'Y'
  ```
表面上看t改变了，其实t的元素并没有变化，变化的是list的元素，所谓的tuple比可变是指tuple所指向的地址不变。


## 控制语句

### if条件判断
if语句的完整形式：
<br>
if condition1:
<br>
    do something
<br>
elif condition2:
<br>
    do something
<br>
elif ...:
<br>
    do something
<br>
else:
 <br>
   do something

```python
birth=input('birth')
if int(birth)<2000:
    print('00前')
else:
    print('00后')
```

### 循环语句
---
* for 循环

* while 循环
<br>
	while (condition is True):
<br>
		do something
---

```python
name=('A','B','C')
for n in name:
	print(n)
#output:'A'
#       'B'
#       'C'

#求1到10之间所有整数之和
sum=0
for i in range(10):   #range(n)产生0到n-1之间的整数序列(0,1,2,...,n-1)
	sum=sum+i+1
```

## dict和set

### dict 
dict的查找速度快，不管有多少元素查找速度都非常快
```python
>>>score={'zhangsan':100,'lisi':80,'wangwu':60}
>>>score['lisi']        #output:80
```
往字典里增加或者修改某key的值，都可以通过dict['key']来实现
```python
>>>score['zhangsan']=90
>>>score['maliu']=95
>>>score    #output:{'zhangsan':90,'lisi':80,'wangwu':60,'maliu':95},不保证元素输出次序
```
通过不存在的key访问dict时，会报错（KeyError),可通过in判断dict是否存在某key,也可通过dict.get(‘key')方法来判断，get返回None表示
<br>
 key不存在，否则返回value.
```python
>>>'Lucy' in score  #output:False
>>>score.get('Lucy')    #output:None
```
删除dict元素，dict.pop('key')
```python
>>>score.pop('maliu')
>>>score    #output:{'zhangsan':90,'lisi':80,'wangwu':60}
```
dict 和list相比：
* 查找和插入的速度极快，不会随着key的数量增加而速度变慢
* 需要占用大量内存，内存浪费大。
所以dict是用空间来换取时间
<br>
注：dict的key为不可变对象，在python中整型和字符串都是不可变对象，可以作为key用。

### set
set是一组key的集合，且key不可重复。
<br>
创建set需要使用list，重复元素被自动过滤掉
<br>
set是无序状态
```python
>>>s=set([1,2,3])
>>>s     #output:{1,2,3}
>>>s2=set([1,1,2,3])
>>>s2   #output:{1,2,3}
```
往set中添加元素，使用set.add(key),存在key执行操作，不会有效果，使用set.remove(key)移除元素
```python
>>>s.add(4)
>>>s        #output:{1,2,3,4}
>>>s.add(1)
>>>s        #output:{1,2,3,4}
>>>s.remove(4)    
>>>s        #outptu:{1,2,3}
```
两个set的并和交
```python
>>>s1=set([1,2,3])
>>>s2=set([2,3,4])
>>>s1&s2       #output:{2,3}
>>>s1|s2       #Output:{1,2,3,4}
```

## 函数的参数

### 位置参数
先看一个例子：
```python
def power(x):
	return x*x
```
对于power(x)函数，x就是一个位置参数

### 默认参数
某些位置或者所有的位置参数都已经给定默认值，当函数调用时，如果传入了相应的参数，则用传入的参数替代默认参数的值，否则使用默认值。
```python
>>>def power(x,n=2):
...    s=1
...    while(n>0):
...		   s=s*x
...		   n=n-1
...	   return s
...
>>>power(2,3)   #output:8
>>>power(2)     #output:4,相当于调用power(2,2)
```
使用默认参数需要注意：
* 必选参数在前面，默认参数在后面，否则python解释器会报错。
* 默认参数必须是不可变对象,否则会出现如下问题
```python
>>>def add_end(L=[]):
...	   L.append('END')
...    return L
...
>>>add_end([1,2,3])        #output:[1,2,3,'END']
>>>add_end(['a','b'])      #output:['a','b','END']
>>>and_end()               #output:['END']
>>>and_end()               #output:['End','END']
```
### 可变参数
可变参数是函数参数前面加*号,如
```python
def calc(*number):
    sum=0
    for n in numbers:
        sum=sum+n*n
    return sum
```
```
>>>calc(1,2)    #output:5
>>>calc()       #output:0
```
可在将一个list或者tuple前面加*转为可变参数
```python
>>>nums=[1,2,3]
>>>calc(*nums)   #output:14
```

### 关键字参数
关键字参数自动在函数内部组装成一个dict.
```python
def person(name,age,**kw):
print('name:'+name,'age:'+age,'other:'+kw)
```
```python
>>>person('Michael',30)  #output:name:Michael age:30 other:{}

#也key传入任意个数的关键字参数：
>>>person('Bob',35,city='Beijing')   #output:name:Bob age:35 other:{'city':'Beijing'}
>>>person('Adam',45,gender='M',job='Engineer')   #output:name:Adam age:45 other:{'gender':'M','job':'Engineer'}
# 可将dict转换乘车关键字参数
>>>kw={'city':'Beijing','job':'Engineer'}
>>>person('Jack',24,**kw)    #output:name:Jack age:24 other:{'city':'Beijing','job':'Engineer'}


### 参数组合
在Python中定义函数，key用必选参数，默认参数，可变参数和关键字参数，这4种参数key一起使用，   
但是参数定义的顺序必须是：必选参数，默认参数，可变参数，关键字参数,如：
```python
def func(a,b,c=0,*args,**kw):
    print('a=',a,'b=',b,'c=',c,'args=',args,'kw=',kw)
```
```python
>>>func(1,2)   #output:a=1 b=2 c=0 args=() kw={}
>>>func(1,2,c=3)  #output:a=1 b=2 c=3 args=() kw={}
>>>func(1,2,3,'a','b')  output:a=1 b=2 c=3 args=('a','b')
>>>func(1,2,3,'a','b',x=99)   #output:a=1 b=2 c=3 args=('a','b') wk={'x':99}

# 最神奇的是通过一个tuple和dict，也可以调用该函数：
>>>args=(1,2,3,4)
>>>kw={'x':99}
>>>func(*args,**kw)   #output:a=1 b=2 c=3 args=(4,) kw={'x':99}
```
因此对于任意函数，都可以通过类似func(*args,**kw)的形式调用它，无论它的参数是如何定义的。



## <a name="Advanced Features"></a> 高级特性
### 切片
用list[i:j]取一个list货tuple的从索引i到索引j之前的元素(不包括索引j元素),当索引从0开始时，可简写成list[:j],比如有如下list:
```python 
>>>L=['Michael','Sarah','Tracy']
#取前3个元素
>>>L[:3]  #output:['Michael','Sarah','Tracy'] 
>>>L[1:3]   #Output:['Sarah','Tracy']
>>>L[-2:]   #output:[Sarah','Tracy']
```
用list[i:j:k]取list索引i到j的元素，步长为k,如：
```python
>>>L=[1,2,3,4,5,6,7,8,9,10]
>>>L=[::5]   #output:[1,6] 
>>>L[:]      #output:[1,2,3,4,5,6,7,8,9,10]
```
字符串也key着是list,每个元素j欧式一个字符，因此，字符串也可以进行切片操作。
```python
>>>'ABCDEFG'[:3]   #ouput:'ABC'
>>>'ABCDEFG'[::2]  #ouput:'ACEG'
```


### 迭代
list或tupele或dict等可迭代对象可通过for ... in 来迭代
```python
>>>d={'a':1,'b':2,'c':3}
>>>for key in d:
...     print(key)   
#output:
a
b
c
```
默认情况下dict迭代的是key，如果要迭代value，可以用for value in d.itervalues()     
同时迭代key和value，用for k,v in d.iteritems().   
字符串也是迭代对象，也可以进行迭代
```python 
for chr in 'ABC':
... print(ch)
...
#output:
A
B
C
 
通过collections模块的Iterable类型来判断一个对象是否为可迭代对象.
```python
>>>from collections import Iterable
>>>isinstance('abc',Iterable)  #str是否可迭代
True
>>>isinstance([1,2,3],Iterable) #list是否可迭代
True
>>>isinstace(123,Iterable) #整数是否可迭代
False
```
pYthon 内置的enumerate函数，key把list变成所以-元素对，这样key同时循环迭代索引和元素值。
```
>>>for i ,value in enumerate(['A','B','C'])
...     print(i,value)
...
0 A
1 B
2 C
```

### 列表生成式
range(i,j)生成从i到j-1的整数list,如
```python
>>>range(0,5)
[0,1,2,3,4]
```
可用list生成其他list,如：
```python
>>>[x*x for x in range(0,5)]
[0,1,4,9,16]
```
同时还可以加上筛选条件：
```python
>>>[x*x for x in range(0,5) if x %2==0]
[0,4,16]
```
还可以用多个list生成list:
```python
>>>[m+n for m in 'ABC' for n in 'XYZ']
['AX','AY','AZ','BX','BY','BZ','CX','CY','CZ']
```
利用列表生成式可以写出非常简洁的代码。如，列出当前目录下的所有文件和目录名。
```python
>>>import os
>>>[d for d in os.listdir('.')]
···

### 生成器
通过列表生成式，可以直接创建一个列表，但是创建一个包含大量元素的列表，要占用很大的存储空间。    
列表元素在访问的过程中按照某种算法推算出，在Python中，一边访问一边计算的机智，称为生成器generator.
创建生成器方法一：列表生成式的[]改成()，就创建了一个generator.
```python
>>>L=[x*x for x in range(10)]
>>>L
[0,1,2,3,4,5,6,7,8,9,10]
>>>g=(x*x for x in range(10))
>>>x
<generator object <genexpr> at 0x1022ef630>
```
generator通过next()获得下一个元素,没有更多元素的时候，抛出StopIteration错误
```python
>>>next(g)
0
>>>next(g)
1
>>>next(g)
4
...
>>>next(g)
81
>>>next(g)
Tracebback (most recent call last):    
  File "<stdin>",lin1,in <module>
  StopIteration
```
generator也是可迭代对象：
```python
>>>g=(x*x for x in range(3))
>>>for n in g:
...     print(n)
...
0
1
4
```

generator生成方法二，函数中包含yield关键字，那么这个函数就是一个generator。
```python
die fib(max):
    n,a,b=0,0,1
    while n<max:
        yield b
        a,b=b,a+b
        n=n+1
    return 'done'
```
```python
>>>f=fib(6)
>>>f
<generator object fib at 0x104feaaa0>
```
yield关键字定义的generator的执行流程为，generator调用next()后，遇到yield语句返回，再次调用后从上次返回的yield语句处继续执行。例如：
```python
def odd():
    print('step 1')
    yield 1
    print('step 2')
    yield 2
    print('step 3')
    yield(5)
```
调用该generator时，先要生成一个generator对象，然后调用next()方法获得下一个返回值。
```python
>>>o =odd()
>>>next(o)
step 1
1
>>>next(o)
step 2
3
>>>next(o)
step 3
5
>>>next(o)
Traceback (most recent call last):
    File "<stdin>",line 1,in <module>
    StopIteration
```
for 循环迭代generator时，无法获得return语句的返回值，要想获得返回值，必须捕获StopIteration，返回值包含在stopIteration的value中。
```python
>>>g=fib(5)
>>>while True:
...     try:
...            x=next(g)
...            print('g:',x)
...        except StopIteration as e:
...            print('Generator return value:'e.value)
...            break
g:1
g:1
g:2
g:3
g:5
g:8
Generator return value:done
```
### 迭代器
可用for循环来迭代的数据类型有：
1. 集合数据类型，如list,tuple,dict,set,str等。
2. generator，包括生成器和带yield的generator function.
这些可for循环遍历的对象都是`可迭代对象`：Iterable.    
使用isinstance()判断一个对象是否为Iterable对象
```python
>>>for collections import Iteralbe
>>>isinstance([],Iterable)
True
>>>isinstance({},Iterable)
True
>>>isinstance('abc',Iterable)
True
>>>isinstance((x for x in range(10)),Iterable)
True
>>>isinstance(100,Iterable)
False
```
可以被next调用并不断返回下一个值的对象称为`迭代器`：Iterator.
使用isinstance()判断一个对象是否为Iterator对象.
```phthon
>>>frome collections import Iterator
>>>isinstance((x for x in range(10)),Iterator)
True
>>>isinstance([],Iterator)
False
>>>isinstance([],Iterator)
False
>>>isinstance({},Iterator)
False
```
生成器都是Iterator对象，但list,dict,str虽然是Iterable，却不是Iterator.    
用iter()把list,dict,str等Iterable变成Iterator。
```python
>>>isinstance(iter([]),Iterator)
True
>>>isinstance(iter('abc'),Iterator)
True
```

## <a name="Functional Programming"></a> 函数式编程
`Functional Programming`,虽也可以归类于面向过程的程序设计，但其思想更接近于计算。    
函数式编程的一个特点是，可以将一个函数作为参数传入另一个函数，且还允许返回一个函数。

### 高阶函数(Higher-order function)
#### 可以将函数赋值给变量

```python
>>>abs(10)
10
>>>abs
<build-in function abs>
>>>f=abs
>>>f
<build-in function abs>
>>>f(10)
10    
# f已经成功指向abs函数本身，直接调用f()和abs()效果是一样的。
```
#### 函数名本身也是变量，也可以将函数名指向其他对象。
```python
# 将abs指向其他对象
>>>abs=10
>>>abs(10)
Traceback (most recent call last):
    File "<stdin>",line 1,in <module>
TypeError:'int' object is not callable
```
注：恢复abs函数，重启python交互环境;要是abs的修改在其他模块生效，要import buildins;buildins.abs=10

#### 传入函数
另一个函数接受一个或多个函数为参数，这种函数称为`高阶函数`.   
一个简单的高阶函数
```python
def add(x,y,f):
    return f(x)+f(y)
```
调用效果：
```
>>>add(-5,5,abs)
10
```

### map和reduce函数
* map()函数接收两个参数，一个是`函数`，一个是`Iterable`,map将传入的函数依次作用到Iterable的每个元素,   
并将作用结果以`Iterator`返回。
举例说明：有一个函数$$ f(x)=x^2  $$,要把这个函数作用到list`[1,2,3,4]的每个元素上，就可以用map实现如下：
```
         f(x)
          |
┌------┬------┬-------┐
1      2      3       4
|      |      |       |
1      4      9       16
```
用python实现如下：
```python
>>>def f(x):
...    return x*x
...
>>>r=map(f,[1,2,3,4])
>>>list(r)
[1,4,9,16]
```
还key把这个list转化为字符串。
```python
>>>list(map(str,[1,2,3,4]))
['1','2','3','4']
```
* reduce()函数，同样接收两个参数，一个函数f和一个list，函数f必须带两个参数，   
reduce把f的返回结果和list的下一个元素继续用f来作用，直到最终结果,其效果如下：   
```
reduce(f,[x1,x2,x3,x4])=f(f(f(x1,x2),x3)x4)   
```
如对序列[1,2,3,4]求和
```python
>>>from functiontool import reduce
>>>def add(x,y):
...     return x+y
...
>>>reduce(add,[1,2,3,4])
10
```
把序列[1,2,3,4]转换成整数1234.
```python
>>>def fn(x,y):
...    return 10*x+y
...
>>>reduce(fn,[1,2,3,4])
1234
```
map和reduce组合用法：将str转换成int(仅仅作map和reduce运用参考)
```python
>>>from functiontool import reduce
>>>def fn(x,y):
...    return 10*x+y
...
>>>def char2num(s):
...    return {'0':0,'1':1,'2':2,'3':3,'4':4,'5':5,'6':6,'7':7,'8':8,'9':9}[s]
...
>>>reduce(fn,map(char2num,'1234'))
1234
```
还key用lambda简化
```python
from functiontool import reduce
def char2num(s):
    return {'0':0,'1':1,'2':2,'3':3,'4':4,'5':5,'6':6,'7':7,'8':8,'9':9}[s]
reduce(lambda x,y:10*x+y,map(char2num,'1234'))
```

### filter
filter()接收一个函数和一个序列，filter()把传入的函数依次作用于每个元素，然后根据返回值是True或者False来   
决定保留还是丢弃该元素。   
如筛选出一个list中的奇数:
```python
def is_odd(n):
    return n%2==1

list(filter(is_odd,[1,2,3,4,5,6]))   #output: [1,3,5]
```
删除一个序列的空字：
```python
def not_empty(s):
    return s and s.strip()

list(filter(ont_empty,['A','','B',None,'C','   ']))  #output:['A','B','C']
```
filter()函数返回的是一个Iterator，使用list()来把结果转化为list.

### sorted 
`排序算法`   
Python内置的sort()函数key对list进行排序。   
```python
>>>sorted([36,5,-12,9,-2])
[-21,-12,5,9,36]
```
此外sort()也是高阶函数，key接收一个`key`函数来实现自定义排序，如按绝对值大小排序：
```python
>>>sorted([36,5,-12,9,-21],key=abs)
[5,9,-12,-21,36]
```
key指定的函数作用于list的每个元素上，并根据key函数返回的结果进行排序。    
对字符串进行排序：
```python
>>>sorted(['bob','about','Zoo','Credit'])
['Credit','Zoo','about','blb']
```
默认情况下，对字符串排序是按ASCII的大小比较的，，‘Z'<'a'，结果Z会排在a前面。     
现在忽略大小写排序：
```python
>>>sorted(['bob','about','Zoo','Credit'],key=str.lower)
['about','bob','Credit','Zoo']
```
进行反向排序时，只需传入第三个参数`reverse=True`:
```python
>>>sorted(['bob','about','Zoo','Credit'],key=str.lower,reverse=True)
['Zoo','Credit','bob','about']
```


### 返回函数
#### 函数作为返回值
高阶函数除了可以接受函数作为参数外，还可以把函数作为结果返回。   
如下：
```python
def lazy_sum(*args):
    def sum():
        ax=0
        for n in args:
            ax=ax+n
        return ax
    return sum
```
当调用lazy_sum()时，返回的不是求和的结果，而是求和函数:
```python
>>>f=lazy_sum(1,3,5,7,9)
>>>f
<function lazy_sum.<locals>.sum at 0x101c6ed90>
```
调用函数f时，才真正进行求和的结果
```python
>>>f()
25
```
在函数lazy_sum中定义了sum,并且sum可以调用外部函数lazy_sum的参数和局部变量，当lazy_sum返回     
函数sum时，相关参数和变量都保存在返回的函数中，这种行为称为`闭包`.    
当掉好用lazy_sum()时，每次调用都会返回一个新的函数，即使传入相同的参数。
```python
>>>f=lazy_sum(1,2,3)
>>>f2=lazy_sum(1,2,3)
>>>f==f2
False
```
f()和f2()的调用结果互不影响。

#### 闭包
例子：
```python
def count():
    fs=[]
    for i in range(1,4):
        def f():
            return i*i
        fs.append(f)
    return fs

f1,f2,f3=count()
```
调用f1(),f2(),f3()想象结果是1，4，9，但实际情况如下：
```python
>>>f1()
9
>>>f2()
9
>>>f3()
9
```
其原因在于返回的函数引用了变量i，但它并不是立即执行，等到3个函数都返回时，变量i的值已经是3,    
因此最终结果是9.    
返回闭包时，返回函数不要引用任何循环变量或者任何后续会发生变化变量。   
一定要引用循环变量的话，可创建一个函数，用该函数的参数绑定循环变量当前值。
```python
def cout():
    def f(j):
        def g():
            return j*j
        return g
    fs=[]
    for i in range(1,4):
        sf.append(f(i))
    return fs
```
运行结果为：
```python
>>>f1,f2,f3=count()
>>>f1()
1
>>>f2()
4
>>>f3()
9
```

### 匿名函数
lambda x:x*x就是匿名函数，关键字lambda表示匿名函数，':'前面的x表示函数参数。   
匿名函数有个限制，就是只能有一个表达式，表达式的结果就是返回值。如    
```python
>>>list(lambda x:x*x ,[1,2,3])
[1,4,9]
```
匿名函数也是函数对象，也可以赋值给变量，再利用变量来调用该函数。 
```python
>>>f=lambda x:x*x
>>>f 
<function <lambda> at 0x101c6ef29>
>>>f(5)
25
```
同样匿名函数也可以作为返回值。
```python
def build(x,y):
    return lambda :x *x+y*y
```

###装饰器
函数也是一个对象，可以将函数变量赋值给变量，通过变量来调用该函数。
```python
>>>def now():
...     print('2017-5-10')
...

>>>f=now
>>>f()
2017-5-10
```
函数对象有一个`__name__`属性，可以取到函数的名字：
```python
>>>now.__name__
'now'
>>>f.__name__
'now'
```
现在假设要增强now()函数的功能，比如在函数调用前后自动打印日志，但又不希望修改now()函数的定义，   
这种在代码运行期间动态增加功能的方式，称之为`装饰器`（Decorator)。   
本质上，decorator是一个返回函数的高级函数。如下定义了一个能打印日志的decorator：
```python
def log(func):
    def wrapper(*args,**kw):
        print('call %s():' % func.__name__)
        return func(*args,**kw)
    return wrapper
```
借助PYthon的@语法，把decorator置于函数的定义处L:
```python
@log
def now():
    print('2017-5-10')
```
调用结果如下：
```python
>>>now()
cal now():
2017-5-10
```
把@log放在now()函数的定义处，相当于执行了语句：
---
now=log(now)
---
如果decorator需要传入一个参数，那就需要编写一个返回decorator的高阶函数，如，要自定义log的文本：
```python
def log(text):
    def decorator(func):
        def wrapper(*args,**kw):
            print('%s %s():' %(text,func.__name__))
            return func(*args,**kw)
        return wrapper
    return decorator
```
用法如下：
```python
@log('execute')
def now():
    print('2017-5-10')
```
执行结果如下：
```python
>>>now()
execute now():
2017-5-10
```
和两层嵌套的decorator相比，3层嵌套的效果是这样的：
```python
>>>now=log('execute')(now)
```
上面的语句先执行log('execute'),返回的是decorator函数，参数是now函数，返回值最终是wrapper函数。    
以上两种decorator函数定义都没有问题，但是函数也是对象,它有__name__等属性，经过decorator装饰后    
的函数，它的__name__已经从原来的'now'变成了'wrapper':
```python
>>>now.__name__
'wrapper'
```
因为返回的那个wrapper()函数名字就是'wrapper',所以需要把原始函数的__name__属性复制到wrapper()函数   
中，否则有些依靠函数签名的代码执行就会出错。不需要编写wrapper.__name__=func.__name__,Python内置   
的functools.wraps就是干这事的，一个完整的decorator的写法如下：
```python
import functools

def log(func):
    @functools.wraps(func)
    def wrapper(*args,**kw):
        print('call %s():' % func.__name__)
        return func(*args,**kw)
    return wrapper
```
或者针对带参数的decorator:
```python
import functools

def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args,**kw):
            print('%s %s():' %(text,func.__name__))
            return func(*args,**kw)
        return wrapper
    return decorator
```

### 偏函数
Python的functools模块提供了很多有用的功能，其中一个就是偏函数。
举例说明偏函数：int()函数把字符串转为整数，当参数为字符串时，int()函数默认按十进制转换：
```python
>>>int('123')
123
```

但是，int()函数还提供额为的base参数，默认值为10，如果传入base参数，就可以作N进制转换：
```python
>>>int('12345',base=8)
5349
>>>int('12345',16)
74565
```
假如要大量的二进制转换，每次都要传入int(x,base2)很麻烦，于是可以定义一个int2()函数，默认把base=2传进去：
```python
def int2(x,base=2):
    return int(x,base)
```
functools.partial就是帮助创建一个相同功能的函数，不需要自己定义int2(),可使用如下代码创建一个新的int2:
```python
>>>import functools
>>>int2=functools.partial(int,base=2)
>>>int2('100000')
64
>>>int2（'1010101'）
85
```
所以简单总结functools.partial的作用就是把一个函数的某些参数固定住，返回一个新的函数。


## <a name="Object_Oriented_Programming"></a> 面向对象编程
### 类和实例
通过关键值`class`定义类：
```python
class Student(object):
    pass
```
class后面紧跟类名，类名通常大写字母开头，object表示继承的类，所有类最终都会继承自object。    
定义好Student类后，可以创建出Student的实例。
```python
>>>bart=Student()
>>>bart
<__main__.Student object at 0x10a67a590>
>>>Student
<class '__main__.Student'>
```
可以自由的给实例变量绑定属性，如实例bart绑定一个name属性：
```python
>>>bart.name='Bart Simpson'
>>>bart.name
'Bart simpson'
```
由于类起到模版作用，可以在创建实例的时候，把一些必须绑定的属性强制填写，通过一个特殊的__init__方法，   
在创建实例的时候，就把name,score等属性绑上去:
···python
class Student(object):
    def __init__(self,name,score):
        self.name=name
        self.score=score
```
__init__方法的第一个参数永远是self，表示创建实例自身，定义了__init__方法，就不能传入空的参数了，   
必须传入__init__方法匹配的参数，self则不需要，Python解释器自己会把实例变量传入进去：
```python
>>>bart=Student('Bart Simpson',59)
>>>bart.name
'Bart Simpson'
>>>bart.score
59
```
### 数据封装
面向对象编程的一个重要特点就是数据封装，通过类内部定义的函数访问数据，这样就把’数据‘给封装起来。
```python
class Student(object):
    def __init__(self,name,score):
        self.name=name
        self.score=score
    
    def print_score(self):
        print('%s: %s' %(self.name,self.score))
```
```python
>>>bart.print_score()
Bart Simpon:59
```

### 访问权限
如果要让类内部属性不被外部访问，可以把属性的名称前面加`__`，在Python中，实例的变量名以`__`开头，    
且不以`__'结尾的就变成一个私有变量(private)。
```python
class Student(object):
    def __init(self,name,score):
        self.__name=name
        self.__score=score

    def print_score(self):
        print('%s ：%s' % (self.__name,self.__score))
```
现在已经不能从外部直接访问.__name和__score了。
```python
>>>bart=Student('Bart Simpson',98)
>>>bart.__name
Traceback (most recent call last):
  File "<stdin>",line 1, in <module>
AttributeError:'Student' object has no attribute '__name'
```
要从外部获取name,score，可以给Student类增加get_name和get_score这样的方法：
```python
class Student(object):
...
def get_name(self):
    return self.__name
def get_score(self):
    return self.__score
```
要修改name和score可以通过set_name，set_score方法：
```python
class Student(object):
    ...
    def set_name(self,name):
        self.__name=name
    def set_score(self,score):
        self.__score=score
```
不能从外部访问私有变量__name,是因为Python解释器把__name改成了_Student__name,所以，仍   
可以通过_Student__name来访问__name变量。但是不同Python解释器会变成不同的名字。    
注：下面的写法是错误的：
```python
>>>bart=Student('Bart SImpson',98)
>>>bart.get_name()
'Bart Simpson'
>>>bart.__name='New Name'
>>>bart.__name
'New Name'
```
表面上看，外部代码’成功‘设置了__name值，但实际上这个__name变量和class内部的__name不是同一个，   
内部的__name已经被Python解释器自动改成了_Student__Name,而外部代码给bart新增了一个__name变量。
```python
>>>bart.get_name()
'Bart Simpson'
```
