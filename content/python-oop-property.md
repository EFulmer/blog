Title: Object-Oriented Programming in Python 1: @property
Date: 2017-07-25
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
 |  
```

`property` is a special builtin class. Instances of property have attributes for getting, setting, and deleting a value. When you make a property, you can define any or all of these attributes; ones that don't get defined default to the standard get/set/delete behavior.

There are two ways to create a property object:
1. Use decorators. Decorators are an advanced Python feature and can look like magic, but using decorators to create a property is more Pythonic.
2. Define the getters, setters, and deleters for your property in the class body, then call `property` like a constructor to create a decorator using your getter and setter.

An example of #2 first:

```
class Ramone(object):
    def __init__(self, name, instrument):
        self.name = name
        self.instrument = instrument

    def countdown_getter(self):
        if not hasattr(self, '_countdown'):
            self._countdown = 1
        return self._countdown

    def countdown_setter(self, new_countdown):
        if new_countdown not in (1, 2, 3, 4):
            raise ValueError('ONE TWO THREE FOUR!')
        self._countdown = new_countdown

    def countdown_deleter(self):
    	print('Today your love, tomorrow the world!')
        del self._countdown

    countdown = property(countdown_getter, countdown_setter, countdown_deleter)
```

Simple, but we'll go through them one-by-one:

* The `getter` only takes a `Ramone`, an instance of the class (`self`), and returns an attribute. It *gets* the attribute. `_countdown` starts with an underscore to signify that there's some extra stuff going on behind the scenes with this attribute -- it's not actually private.
* The `setter` needs to take `self` and a value to update the attribute with. No return, because the computation is changing an attribute on `self`. For the sake of historical accuracy, Ramones can only count to four.
* The `deleter` deletes the attribute. Simple... though `del` is a little less obvious than it sounds, but we'll tackle that in the future.

This example bothers me because `countdown_getter`, `setter`, and `deleter` are all still visible and callable under those names. The purpose of defining them may not be immediately clear to readers of the code until they get to the line where `property` is called.

Here's the decorator version:

```
class Ramone(object):
    def __init__(self, name, instrument):
        self.name = name
        self.instrument = instrument
    
    @property
    def countdown(self):
        if not hasattr(self, '_countdown'):
            self._countdown = 1
        return self._countdown

    @countdown.setter
    def countdown(self, new_countdown):
        if new_countdown not in (1, 2, 3, 4):
            raise ValueError("ONE TWO THREE FOUR!")
        self._countdown = new_countdown

    @countdown.deleter
    def countdown(self):
        del self._countdown
```

This version is clearer because you can see that `countdown` is a property as soon as you read the decorator syntax and the method header. The decorator syntax may look a little strange to new Python programmers. 

The gist of what it does is that the name following the `@` sign is a function's name. That function gets used to "decorate" the function you define, augmenting it with additional behavior. In this case, the function gets the get/set/delete machinery added to it.

We'll come back to hiding data inside objects later. Next time, we continue looking at how we can override attribute access and modification.
