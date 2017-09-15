---
layout: post
title:  Python装饰器
categories: Python 
tags:  装饰器
mathjax: true
---

* content
{:toc}

装饰器本质上是一个Python函数，它可以让其他函数在不需要做任何代码变动的前提下增加额外功能，装饰器的返回值也是一个函数对
象。它经常用于有切面需求的场景，比如：插入日志、性能测试、事务处理、缓存、权限校验等场景。装饰器是解决这类问题的绝佳设
计，有了装饰器，我们就可以抽离出大量与函数功能本身无关的雷同代码并继续重用。概括的讲，装饰器的作用就是为已经存在的函数或对象添加额外的功能。





### 基于函数实现的装饰器

#### 无参数装饰器

```python
# encoding: utf-8

def my_decorator(func):
    print("这是无参数的装饰器")
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def add(a, b):
    return a+b

print(add(6, 8))
```

输出：

```
这是无参数的装饰器
14
```

#### 带参装饰器

```python
# encoding: utf-8

def my_decorator(canshu = "happy"):
    print("这是带参数的装饰器:", canshu)
    def wrapper(func):
        def inner_wrapper(*args, **kwargs):
            return func(*args, **kwargs)
        return inner_wrapper
    return wrapper

@my_decorator(canshu = "hello world")
def add(a, b):
    return a+b

print(add(6, 8))
```

输出：

```
这是带参数的装饰器: hello world
14
```

### 基于类实现的装饰器

装饰器函数其实是这样一个接口约束，它必须接受一个callable对象作为参数，然后返回一个callable对象。在Python中一般callable对象都是函数，但也有例外。
只要某个对象重载了__call__()方法，那么这个对象就是callable的，可以像函数那样被调用。

#### 无参数的类装饰器

```python
# encoding: utf-8
class logging(object):
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print("[DEBUG]: enter function {func}()".format(
            func=self.func.__name__))
        return self.func(*args, **kwargs)
@logging
def say(something):
    print("say {}!".format(something))

say("hello world")
```

输出：

```
[DEBUG]: enter function say()
say hello world!
```

#### 带参数的类装饰器

如果需要通过类形式实现带参数的装饰器，那么会比前面的例子稍微复杂一点。那么在构造函数里接受的就不是一个函数，而是传入的参数。通过类把这些参数保存起来。
然后在重载`__call__`方法是就需要接受一个函数并返回一个函数。

```python
# encoding: utf-8
class logging(object):
    def __init__(self, level='INFO'):
        self.level = level

    def __call__(self, func):  # 接受函数
        def wrapper(*args, **kwargs):
            print("[{level}]: enter function {func}()".format(
                level=self.level,
                func=func.__name__))
            func(*args, **kwargs)
        return wrapper  # 返回函数


@logging(level='INFO')
def say(something):
    print("say {}!".format(something))

say("hello world")
```

输出:

```
[INFO]: enter function say()
say hello world!
```

### 内置的装饰器

```@property @staticmethod @classmethod  @abstractmehod ...```返回的分别是property、staticmethod、classmethod、abstractmehod类对象。


### 补充

```python
# encoding: utf-8

def my_decorator(func):
    print("这是无参数的装饰器")
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def add(a, b):
    print("hello")
    return a+b
print(add(6,8))
print("------")
print(my_decorator(add(6, 8)))
```

输出：

```
这是无参数的装饰器
hello
14
------
hello
这是无参数的装饰器
<function my_decorator.<locals>.wrapper at 0x0000000002598EA0>

```

可以发现，两者的输出是有区别的。

decorator和wrapt两个模块可以优化装饰器代码。

python中的静态方法，相当于将其重新包装成staticmethod类的实例，所以不再依赖于原有类的对象的存在而存在。？？？

staticmethod类中的new方法用@staticmethod修饰，不会造成循环递归吗？




