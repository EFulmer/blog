Title: Object-Oriented Programming in Python 2: __getattr__
Date: 2017-08-22
Category: Programming
Tags: Python, OOP, Datamodel

In this installment of our ongoing investigation of the Python model for object-oriented programming, we will be investigating the `__xattr__` methods: `__getattribute__`, `__setattr__`, and `__getattr__`.

If defined for a class, `__getattribute__` is expcted to have a signature of `__getattr__(self, name)`. It should return `self.name` and handle any additional logic around attribute access your class requires. 

The biggest pitfall Python programmers beginning exploration of special data model functions make is falling into the infinite recursion trap. Since `__getattribute__` overrides attribute access, any `self.attr` expressions get translated into `self.__getattr__(attr)`. So, if you access an attribute with dot notation inside of `__getattr__`, you will end up getting a `RecursionError`. 
