---
layout: post
title:  ABCMeta和super
categories: Python 
tags:  ABCMeta  super
mathjax: true
---

* content
{:toc}

抽象类的意义可参考PEP3119：[Abstract Base Classes](http://legacy.python.org/dev/peps/pep-3119/)。





### ABCMeta

ABCMeta在abc(abstract base classes)模块中，是所有抽象类的元类，其源码如下：

```python
class ABCMeta(type):

    """Metaclass for defining Abstract Base Classes (ABCs).

    Use this metaclass to create an ABC.  An ABC can be subclassed
    directly, and then acts as a mix-in class.  You can also register
    unrelated concrete classes (even built-in classes) and unrelated
    ABCs as 'virtual subclasses' -- these and their descendants will
    be considered subclasses of the registering ABC by the built-in
    issubclass() function, but the registering ABC won't show up in
    their MRO (Method Resolution Order) nor will method
    implementations defined by the registering ABC be callable (not
    even via super()).

    """

    # A global counter that is incremented each time a class is
    # registered as a virtual subclass of anything.  It forces the
    # negative cache to be cleared before its next use.
    # Note: this counter is private. Use `abc.get_cache_token()` for
    #       external code.
    _abc_invalidation_counter = 0

    def __new__(mcls, name, bases, namespace):
        cls = super().__new__(mcls, name, bases, namespace)
        # Compute set of abstract method names
        abstracts = {name
                     for name, value in namespace.items()
                     if getattr(value, "__isabstractmethod__", False)}
        for base in bases:
            for name in getattr(base, "__abstractmethods__", set()):
                value = getattr(cls, name, None)
                if getattr(value, "__isabstractmethod__", False):
                    abstracts.add(name)
        cls.__abstractmethods__ = frozenset(abstracts)
        # Set up inheritance registry
        cls._abc_registry = WeakSet()
        cls._abc_cache = WeakSet()
        cls._abc_negative_cache = WeakSet()
        cls._abc_negative_cache_version = ABCMeta._abc_invalidation_counter
        return cls

    def register(cls, subclass):
        """Register a virtual subclass of an ABC.

        Returns the subclass, to allow usage as a class decorator.
        """
        if not isinstance(subclass, type):
            raise TypeError("Can only register classes")
        if issubclass(subclass, cls):
            return subclass  # Already a subclass
        # Subtle: test for cycles *after* testing for "already a subclass";
        # this means we allow X.register(X) and interpret it as a no-op.
        if issubclass(cls, subclass):
            # This would create a cycle, which is bad for the algorithm below
            raise RuntimeError("Refusing to create an inheritance cycle")
        cls._abc_registry.add(subclass)
        ABCMeta._abc_invalidation_counter += 1  # Invalidate negative cache
        return subclass

    def _dump_registry(cls, file=None):
        """Debug helper to print the ABC registry."""
        print("Class: %s.%s" % (cls.__module__, cls.__qualname__), file=file)
        print("Inv.counter: %s" % ABCMeta._abc_invalidation_counter, file=file)
        for name in sorted(cls.__dict__.keys()):
            if name.startswith("_abc_"):
                value = getattr(cls, name)
                print("%s: %r" % (name, value), file=file)

    def __instancecheck__(cls, instance):
        """Override for isinstance(instance, cls)."""
        # Inline the cache checking
        subclass = instance.__class__
        if subclass in cls._abc_cache:
            return True
        subtype = type(instance)
        if subtype is subclass:
            if (cls._abc_negative_cache_version ==
                ABCMeta._abc_invalidation_counter and
                subclass in cls._abc_negative_cache):
                return False
            # Fall back to the subclass check.
            return cls.__subclasscheck__(subclass)
        return any(cls.__subclasscheck__(c) for c in {subclass, subtype})

    def __subclasscheck__(cls, subclass):
        """Override for issubclass(subclass, cls)."""
        # Check cache
        if subclass in cls._abc_cache:
            return True
        # Check negative cache; may have to invalidate
        if cls._abc_negative_cache_version < ABCMeta._abc_invalidation_counter:
            # Invalidate the negative cache
            cls._abc_negative_cache = WeakSet()
            cls._abc_negative_cache_version = ABCMeta._abc_invalidation_counter
        elif subclass in cls._abc_negative_cache:
            return False
        # Check the subclass hook
        ok = cls.__subclasshook__(subclass)
        if ok is not NotImplemented:
            assert isinstance(ok, bool)
            if ok:
                cls._abc_cache.add(subclass)
            else:
                cls._abc_negative_cache.add(subclass)
            return ok
        # Check if it's a direct subclass
        if cls in getattr(subclass, '__mro__', ()):
            cls._abc_cache.add(subclass)
            return True
        # Check if it's a subclass of a registered class (recursive)
        for rcls in cls._abc_registry:
            if issubclass(subclass, rcls):
                cls._abc_cache.add(subclass)
                return True
        # Check if it's a subclass of a subclass (recursive)
        for scls in cls.__subclasses__():
            if issubclass(subclass, scls):
                cls._abc_cache.add(subclass)
                return True
        # No dice; update negative cache
        cls._abc_negative_cache.add(subclass)
        return False
```

#### 重写built-in函数中isinstance()和issubclass()

当调用isinstance(x,C)时，首先检查C.__instance__存不存在，如果存在，则调用C.instance(x);
issubclass()同样。

```python
class ABCMeta(type):

    def __instancecheck__(cls, inst):
        """Implement isinstance(inst, cls)."""
        return any(cls.__subclasscheck__(c)
                   for c in {type(inst), inst.__class__})

    def __subclasscheck__(cls, sub):
        """Implement issubclass(sub, cls)."""
        candidates = cls.__dict__.get("__subclass__", set()) | {cls}
        return any(c in candidates for c in sub.mro())

class Sequence(metaclass=ABCMeta):
    __subclass__ = {list, tuple}

assert issubclass(list, Sequence)
assert issubclass(tuple, Sequence)

class AppendableSequence(Sequence):
    __subclass__ = {list}

assert issubclass(list, AppendableSequence)
assert isinstance([], AppendableSequence)

assert not issubclass(tuple, AppendableSequence)
assert not isinstance((), AppendableSequence)
```

用处：如上可以用抽象类定义一个新的抽象类。

### abstractmethod

```python
# encoding: utf-8
from abc import  ABCMeta, abstractmethod
class AbstractTest(metaclass=ABCMeta):
    # 抽象方法可以有具体的函数实现，可以被子类通过super()调用
    @abstractmethod
    def add(self, a, b):
        return a+b

    def sub(self):
        print("world")

class Test(AbstractTest):
    def __init__(self, a, b):
        self.a = a
        self.b = b
    def add(self):
        print(super().add(self.a, self.b))
        print("hello")

test = Test(4, 8)
test.add()
test.sub()
```

输出：

```
12
hello
world
```

### super()

super也是一个built-in类，调用父类的顺序按照mro顺序。