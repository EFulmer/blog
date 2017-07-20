Title: Object-Oriented Programming in Python 1: @property
Date: 2017-07-17
Category: Programming

Coming from Java, one of the things that initially confused me about Python was the lack of private attributes, getters, and setters. How were you supposed to control access to your objects' inner workings?

Even if you don't come from a language with private member variables, you might still ask the same question about hiding your objects' inner machinery from other programmers.

Obviously, Python's design philosophy is vastly different than Java's. While information hiding isn't really supported (though there are easily available language mechanisms that *discourage* other programmers from touching object attributes), you _can_ create getters and setters for attributes.

You turn an attribute from an ordinary Python object into one treated as a special class attribute, with unique getter, setter, and deleter behavior by creating a `property` object.

From the documentation:

```
class property(object)
 |  property(fget=None, fset=None, fdel=None, doc=None) -> property attribute
 |
 |  fget is a function to be used for getting an attribute value, and likewise
 |  fset is a function for setting, and fdel a function for del'ing, an
 |  attribute.  Typical use is to define a managed attribute x:
 ```

property is a special builtin class. Instances of property have attributes for getting, setting, and deleting a value. You can use any of these attributes; ones that don't get defined default to the standard get/set/delete behavior.
