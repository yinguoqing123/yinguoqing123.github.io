---
layout: post
title:  "Python魔法方法"
categories: Python
tags:  Python 魔法方法
mathjax: true
---

* content
{:toc}

Python内的built-in方法实际上是用C语言实现的，当使用built-in方法时，实际上调用类内的魔法方法，因此
可以通过重写类内的魔法方法，改变built-in方法的行为。




### 魔法方法

<style> 
.red{color:#F00} 
</style> 
<table class="t_table " cellspacing="0">
<tbody>
<tr>
<td>
<div align="center">魔法方法</div>


</td>
<td>
<div align="center">含义</div>


</td>


</tr>
<tr>
<td>&nbsp;</td>
<td>
<div class="red" align="left">基本的魔法方法</div>


</td>


</tr>
<tr>
<td>__new__(cls[, ...])</td>
<td>1. __new__ 是在一个对象实例化的时候所调用的第一个方法<br>2. 它的第一个参数是这个类，其他的参数是用来直接传递给 __init__ 方法<br>3. __new__ 决定是否要使用该 __init__ 方法，因为 __new__ 可以调用其他类的构造方法或者直接返回别的实例对象来作为本类的实例，如果 __new__ 没有返回实例对象，则 __init__ 不会被调用<br>4. __new__ 主要是用于继承一个不可变的类型比如一个 tuple 或者 string</td>


</tr>
<tr>
<td>__init__(self[, ...])</td>
<td>构造器，当一个实例被创建的时候调用的初始化方法</td>


</tr>
<tr>
<td>__del__(self)</td>
<td>析构器，当一个实例被销毁的时候调用的方法</td>


</tr>
<tr>
<td>__call__(self[, args...])</td>
<td>允许一个类的实例像函数一样被调用：x(a, b) 调用 x.__call__(a, b)</td>


</tr>
<tr>
<td>__len__(self)</td>
<td>定义当被 len() 调用时的行为</td>


</tr>
<tr>
<td>__repr__(self)</td>
<td>定义当被 repr() 调用时的行为</td>


</tr>
<tr>
<td>__str__(self)</td>
<td>定义当被 str() 调用时的行为</td>


</tr>
<tr>
<td>__bytes__(self)</td>
<td>定义当被 bytes() 调用时的行为</td>


</tr>
<tr>
<td>__hash__(self)</td>
<td>定义当被 hash() 调用时的行为</td>


</tr>
<tr>
<td>__bool__(self)</td>
<td>定义当被 bool() 调用时的行为，应该返回 True 或 False</td>


</tr>
<tr>
<td>__format__(self, format_spec)</td>
<td>定义当被 format() 调用时的行为</td>


</tr>
<tr>
<td>&nbsp;</td>
<td><font color="#FF0000">有关属性</font></td>


</tr>
<tr>
<td>__getattr__(self, name)</td>
<td>定义当用户试图获取一个不存在的属性时的行为</td>


</tr>
<tr>
<td>__getattribute__(self, name)</td>
<td>定义当该类的属性被访问时的行为</td>


</tr>
<tr>
<td>__setattr__(self, name, value)</td>
<td>定义当一个属性被设置时的行为</td>


</tr>
<tr>
<td>__delattr__(self, name)</td>
<td>定义当一个属性被删除时的行为</td>


</tr>
<tr>
<td>__dir__(self)</td>
<td>定义当 dir() 被调用时的行为</td>


</tr>
<tr>
<td>__get__(self, instance, owner)</td>
<td>定义当描述符的值被取得时的行为</td>


</tr>
<tr>
<td>__set__(self, instance, value)</td>
<td>定义当描述符的值被改变时的行为</td>


</tr>
<tr>
<td>__delete__(self, instance)</td>
<td>定义当描述符的值被删除时的行为</td>


</tr>
<tr>
<td>&nbsp;</td>
<td><font color="#FF0000">比较操作符</font></td>


</tr>
<tr>
<td>__lt__(self, other)</td>
<td>定义小于号的行为：x &lt; y 调用 x.__lt__(y)</td>


</tr>
<tr>
<td>__le__(self, other)</td>
<td>定义小于等于号的行为：x &lt;= y 调用 x.__le__(y)</td>


</tr>
<tr>
<td>__eq__(self, other)</td>
<td>定义等于号的行为：x == y 调用 x.__eq__(y)</td>


</tr>
<tr>
<td>__ne__(self, other)</td>
<td>定义不等号的行为：x != y 调用 x.__ne__(y)</td>


</tr>
<tr>
<td>__gt__(self, other)</td>
<td>定义大于号的行为：x &gt; y 调用 x.__gt__(y)</td>


</tr>
<tr>
<td>__ge__(self, other)</td>
<td>定义大于等于号的行为：x &gt;= y 调用 x.__ge__(y)</td>


</tr>
<tr>
<td>&nbsp;</td>
<td><font color="#FF0000">算数运算符</font></td>


</tr>
<tr>
<td>__add__(self, other)</td>
<td>定义加法的行为：+</td>


</tr>
<tr>
<td>__sub__(self, other)</td>
<td>定义减法的行为：-</td>


</tr>
<tr>
<td>__mul__(self, other)</td>
<td>定义乘法的行为：*</td>


</tr>
<tr>
<td>__truediv__(self, other)</td>
<td>定义真除法的行为：/</td>


</tr>
<tr>
<td>__floordiv__(self, other)</td>
<td>定义整数除法的行为：//</td>


</tr>
<tr>
<td>__mod__(self, other)</td>
<td>定义取模算法的行为：%</td>


</tr>
<tr>
<td>__divmod__(self, other)</td>
<td>定义当被 divmod() 调用时的行为</td>


</tr>
<tr>
<td>__pow__(self, other[, modulo])</td>
<td>定义当被 power() 调用或 ** 运算时的行为</td>


</tr>
<tr>
<td>__lshift__(self, other)</td>
<td>定义按位左移位的行为：&lt;&lt;</td>


</tr>
<tr>
<td>__rshift__(self, other)</td>
<td>定义按位右移位的行为：&gt;&gt;</td>


</tr>
<tr>
<td>__and__(self, other)</td>
<td>定义按位与操作的行为：&amp;</td>


</tr>
<tr>
<td>__xor__(self, other)</td>
<td>定义按位异或操作的行为：^</td>


</tr>
<tr>
<td>__or__(self, other)</td>
<td>定义按位或操作的行为：|</td>


</tr>
<tr>
<td>&nbsp;</td>
<td><font color="#FF0000">反运算</font></td>


</tr>
<tr>
<td>__radd__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rsub__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rmul__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rtruediv__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rfloordiv__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rmod__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rdivmod__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rpow__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rlshift__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rrshift__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__rxor__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>__ror__(self, other)</td>
<td>（与上方相同，当左操作数不支持相应的操作时被调用）</td>


</tr>
<tr>
<td>&nbsp;</td>
<td><font color="#FF0000">增量赋值运算</font></td>


</tr>
<tr>
<td>__iadd__(self, other)</td>
<td>定义赋值加法的行为：+=</td>


</tr>
<tr>
<td>__isub__(self, other)</td>
<td>定义赋值减法的行为：-=</td>


</tr>
<tr>
<td>__imul__(self, other)</td>
<td>定义赋值乘法的行为：*=</td>


</tr>
<tr>
<td>__itruediv__(self, other)</td>
<td>定义赋值真除法的行为：/=</td>


</tr>
<tr>
<td>__ifloordiv__(self, other)</td>
<td>定义赋值整数除法的行为：//=</td>


</tr>
<tr>
<td>__imod__(self, other)</td>
<td>定义赋值取模算法的行为：%=</td>


</tr>
<tr>
<td>__ipow__(self, other[, modulo])</td>
<td>定义赋值幂运算的行为：**=</td>


</tr>
<tr>
<td>__ilshift__(self, other)</td>
<td>定义赋值按位左移位的行为：&lt;&lt;=</td>


</tr>
<tr>
<td>__irshift__(self, other)</td>
<td>定义赋值按位右移位的行为：&gt;&gt;=</td>


</tr>
<tr>
<td>__iand__(self, other)</td>
<td>定义赋值按位与操作的行为：&amp;=</td>


</tr>
<tr>
<td>__ixor__(self, other)</td>
<td>定义赋值按位异或操作的行为：^=</td>


</tr>
<tr>
<td>__ior__(self, other)</td>
<td>定义赋值按位或操作的行为：|=</td>


</tr>
<tr>
<td>&nbsp;</td>
<td><font color="#FF0000">一元操作符</font></td>


</tr>
<tr>
<td>__neg__(self)</td>
<td>定义正号的行为：+x</td>


</tr>
<tr>
<td>__pos__(self)</td>
<td>定义负号的行为：-x</td>


</tr>
<tr>
<td>__abs__(self)</td>
<td>定义当被 abs() 调用时的行为</td>


</tr>
<tr>
<td>__invert__(self)</td>
<td>定义按位求反的行为：~x</td>


</tr>
<tr>
<td>&nbsp;</td>
<td><font color="#FF0000">类型转换</font></td>


</tr>
<tr>
<td>__complex__(self)</td>
<td>定义当被 complex() 调用时的行为（需要返回恰当的值）</td>


</tr>
<tr>
<td>__int__(self)</td>
<td>定义当被 int() 调用时的行为（需要返回恰当的值）</td>


</tr>
<tr>
<td>__float__(self)</td>
<td>定义当被 float() 调用时的行为（需要返回恰当的值）</td>


</tr>
<tr>
<td>__round__(self[, n])</td>
<td>定义当被 round() 调用时的行为（需要返回恰当的值）</td>


</tr>
<tr>
<td>__index__(self)</td>
<td>1. 当对象是被应用在切片表达式中时，实现整形强制转换<br>2. 如果你定义了一个可能在切片时用到的定制的数值型,你应该定义 __index__<br>3. 如果 __index__ 被定义，则 __int__ 也需要被定义，且返回相同的值</td>


</tr>
<tr>
<td>&nbsp;</td>
<td><font color="#FF0000">上下文管理（with 语句）</font></td>


</tr>
<tr>
<td>__enter__(self)</td>
<td>1. 定义当使用 with 语句时的初始化行为<br>2. __enter__ 的返回值被 with 语句的目标或者 as 后的名字绑定</td>


</tr>
<tr>
<td>__exit__(self, exc_type, exc_value, traceback)</td>
<td>1. 定义当一个代码块被执行或者终止后上下文管理器应该做什么<br>2. 一般被用来处理异常，清除工作或者做一些代码块执行完毕之后的日常工作</td>


</tr>
<tr>
<td>&nbsp;</td>
<td><font color="#FF0000">容器类型</font></td>


</tr>
<tr>
<td>__len__(self)</td>
<td>定义当被 len() 调用时的行为（返回容器中元素的个数）</td>


</tr>
<tr>
<td>__getitem__(self, key)</td>
<td>定义获取容器中指定元素的行为，相当于 self[key]</td>


</tr>
<tr>
<td>__setitem__(self, key, value)</td>
<td>定义设置容器中指定元素的行为，相当于 self[key] = value</td>


</tr>
<tr>
<td>__delitem__(self, key)</td>
<td>定义删除容器中指定元素的行为，相当于 del self[key]</td>


</tr>
<tr>
<td>__iter__(self)</td>
<td>定义当迭代容器中的元素的行为</td>


</tr>
<tr>
<td>__reversed__(self)</td>
<td>定义当被 reversed() 调用时的行为</td>


</tr>
<tr>
<td>__contains__(self, item)</td>
<td>定义当使用成员测试运算符（in 或 not in）时的行为</td>


</tr>


</tbody>


</table>

```python
dir(object)
```
输出：

['\_\_class\_\_', '\_\_delattr\_\_', '\_\_dir\_\_', '\_\_doc\_\_', '\_\_eq\_\_', '\_\_format\_\_', '\_\_ge\_\_', 
'\_\_getattribute\_\_', '\_\_gt\_\_', '\_\_hash\_\_', '\_\_init\_\_', '\_\_init_subclass\_\_', '\_\_le\_\_', '\_\_lt\_\_', '\_\_ne\_\_', '\_\_new\_\_', '\_\_reduce\_\_', 
'\_\_reduce\_ex\_\_', '\_\_repr\_\_', '\_\_setattr\_\_', '\_\_sizeof\_\_', '\_\_str\_\_', '\_\_subclasshook\_\_']

dir(type)的输出和上面不一样，type和object属于先有鸡还是先有蛋的关系。

