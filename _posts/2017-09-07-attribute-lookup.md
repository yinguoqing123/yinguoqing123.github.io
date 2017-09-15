---
layout: post
title:  Python属性查找顺序
categories: Python 
tags:  属性查找
mathjax: true
---

* content
{:toc}

当对象调用一个属性时，是如何寻找改属性的？





### Python描述符(descriptor)


用处：

类型检查：如类中的每个对象都用一个email属性，需要预先检查email值的格式是否正确。

调用：

对于类属性描述符对象，使用Classname.__getattribute__，它能把Class.x转换成Classname.__dict__[‘x’].__get__(None, Classname)。
对于实例属性描述符对象，使用instancename.__getattribute__，它能把object.x转换为type(instancename).__dict__[‘x’].__get__(instancename, type(instancename))。

#### `__getattr__()、__getattribute__()`

`object.__getattr__(self, name)`当一般位置找不到attribute的时候，会调用getattr，返回一个值或AttributeError异常.
`object.__getattribute__(self, name) `
无条件被调用，通过实例访问属性。如果class中定义了`__getattribute__()`，则`__getattr__()`不会被调用（除非显示调用或引发AttributeError异常）

示例:

```python
class A():
    def __init__(self):
        pass
    def __getattr__(self, item):
        print("该属性不存在")
    '''
    def __getattribute__(self, item):
        print("在调用任何属性之前调用")
    '''

a = A()
a.z
``` 

输出：

```
该属性不存在
```

去掉`__getattribute__()`注释后输出：

```
在调用任何属性之前调用
```

object类中的`__getattribute__()`方法是：

```python
def __getattribute__(self, *args, **kwargs): # real signature unknown
        """ Return getattr(self, name). """
        pass
```

#### `__get__()`、类属性
 
python描述符是一个“绑定行为”的对象属性，在描述符协议中，它可以通过方法重写属性的访问。这些方法有` __get__(), __set__(), 和__delete__()`。
如果这些方法中的任何一个被定义在一个对象中，这个对象就是一个描述符。 

定义一个描述符：

```python
# encoding: utf-8

#描述符类
class Descriptor():
    def __init__(self, x):
        self.x = x
    def __get__(self, instance, owner):
        print("实现描述符的get")
        return  self.x
    def __set__(self, instance, value):
        print("实现描述符的set")
        self.x = value
    def __delete__(self, instance):
        print("实现描述符的delete")
        del self.x

class A():
    x  = Descriptor(10)

a = A()
a.x
A.__dict__["x"].__get__(None,A)
a.x = 8
del a.x
```

输出：

```
实现描述符的get
实现描述符的get
实现描述符的set
实现描述符的delete
```

访问属性时，*既可以通过类访问，也可以通过对象访问*，但是当没有set方法时，当重新给a.x赋值时，a.x是一个新变量，a.x和A.x不同，可通过id函数查看。具体原因是
因为python中一切都是对象，对于不可变对象，改变值等同于新建了一个新对象。
解析器发现x是一个描述符，通过`A.__getattr__()`将A.x转化为`A.__dict__[“x”].__get__(None,A)`来访问

#### `__get__()`、对象属性

如果将一个对象属性设置为描述符，效果如何？

```python
# encoding: utf-8

#描述符类
class Descriptor():
    def __init__(self, x):
        self.x = x
    def __get__(self, instance, owner):
        print("实现描述符的get")
        return  self.x
    def __set__(self, instance, value):
        print("实现描述符的set")
        self.x = value
    def __delete__(self, instance):
        print("实现描述符的delete")
        del self.x

class A():
    def __init__(self, x, y):
        self.x  = Descriptor(x)
        self.y = y

a = A(10, 8)
print("a.x的value：", a.x)
print("a.y的value：", a.y)
print("a.x的ID：",id(a.x))
a.x = 5
a.y = 4
print("a.x的value：",a.x)
print("a.y的value：", a.y)
print("a.x的ID：", id(a.x))
print("a.y的ID：", id(a.y))
```

输出：

```
a.x的value： <__main__.Descriptor object at 0x000000000255D080>
a.y的value： 8
a.x的ID： 39178368
a.x的value： 5
a.y的value： 4
a.x的ID： 1888400576
a.y的ID： 1888400544
```

首先访问对象属性没有触发描述符，其次int是不可变对象，a.x = 5 等同于将a.x与一个新的int对象绑定。其次访问顺序是`a.__getattribute__`,会将a.x转换为`type(a).__dict__[‘x’].__get__(a,type(a))`，不存在,再去寻找`a.__dict__["x"]`.

如果类属性描述符和对象属性同名？

```python
# encoding: utf-8

#描述符类
class Descriptor():
    def __init__(self, x):
        self.x = x
    def __get__(self, instance, owner):
        print("实现描述符的get")
        return  self.x
    def __set__(self, instance, value):
        print("实现描述符的set")
        self.x = value
    def __delete__(self, instance):
        print("实现描述符的delete")
        del self.x

class A():
    x =  Descriptor(10)
    def __init__(self, x):
        self.x  = x

a = A(5)
a.x
```

输出：

```
实现描述符的set
实现描述符的get
```

首先初始化时，寻找x属性，通过`a.__getattribute__()`将self.x转化为`type(a).__dict__["x"].__set__()`,在`A.__dict__`中
x属性存在，所以调用了描述符方法，简而言之，类中的x属性覆盖了实例的x属性。

但是如果类描述符属性只实现了`__get__()`方法，即描述符是非数据描述符，输出如何？

```py
# encoding: utf-8

#描述符类
class Descriptor():
    def __init__(self, x):
        self.x = x
    def __get__(self, instance, owner):
        print("实现描述符的get")
        return  self.x
    '''
    def __set__(self, instance, value):
        print("实现描述符的set")
        self.x = value
    def __delete__(self, instance):
        print("实现描述符的delete")
        del self.x
    '''

class A():
    x =  Descriptor(10)
    def __init__(self, x):
        self.x  = x

a = A(5)
print(a.x)
A.x

# 需要连__delete__()也注释掉，否则出错 
# 输出：  5  实现描述符的get
```

可见，非数据描述符不会覆盖实例属性，可理解为初始化x需要x描述符实现`__set__()`方法，但`A.__dict__["x"]`
对象没有实现`__set__()`方法，所以认为两者不是一个对象。

### 属性查找顺序

如果obj是某个类的实例，那么obj.name首先调用`__getattribute__`。如果类定义了`__getattr__`方法，那么在`__getattribute__`抛出 AttributeError 
的时候就会调用到`__getattr__`，而对于描述符(`__get__`）的调用，则是发生在`__getattribute__`内部的。官网文档是这么描述的

>The implementation works through a precedence chain that gives data descriptors priority over instance variables, 
instance variables priority over non-data descriptors, 
>and assigns lowest priority to `__getattr__()` if provided.

假设我们有个类A,其中a是A的实例，a.x时发生了什么?属性的lookup顺序如下:

获取type(a),调用`A.__getattribute__`,在`a.__getattribute__`内部查找顺序为：

1. 通过A.mro获取A的父类顺序，依顺序寻找`ClassParent.__dict__`，若有属性x，且x为*数据*描述符，则调用
`ClassParent.__dict__["x"].__get__()`方法。否则进行第二步。
2. 查找`a.__dict__`,若存在属性x，(无论是数据描述符，非数据描述符，或普通属性)，则返回，否则第三步。
3. 按照A.mro的顺序，查找`ClassParent.__dict__`，若存在属性x，若属性x为非数据描述符，调用
`ClassParent.__dict__["x"].__get__()`；若x为普通属性，则返回值；若不存在属性x，继续。
4. 若A中有`__getattr__()`,调用该方法
5. 抛出AttributeError

A.x时发生了什么？属性的lookup顺序如下：

首先获取A的metaclass，和metaclass中的`__getattribute__()`方法，调用`__getattribute__()`方法，在`__getattribute__()`
内部的查找顺序：

1. metaclass的mro父类顺序，按顺序在父类字典中寻找是否存在属性x，且x为*数据*描述符，存在则调用`__get__()`方法，否则往下。
2. 在class或其父类中，寻找属性x，找到则返回(无论是数据描述符，非数据描述符，或普通属性)
3. metaclass的mro父类顺序，寻找属性x(x只能为非数据描述符或普通属性)，若不存在，往下
4. 调用metaclass中的`__getattr__()`
5. 抛出AttributeError

一个描述符的很好的例子是property类，使用描述符也可以实现@classmethod,@staticmethod

### 参考文章

* [http://www.betterprogramming.com/object-attribute-lookup-in-python.html](http://www.betterprogramming.com/object-attribute-lookup-in-python.html)

* [https://docs.python.org/3/howto/descriptor.html](https://docs.python.org/3/howto/descriptor.html)







