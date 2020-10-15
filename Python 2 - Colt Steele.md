

## Iterators vs Generators


####_Iterators_


*An __Iterator is an object that can be iterated upon__. An object which returns data, one element at a time when ```next()``` is called on it*

i.e: 
>*"HELLO"* is an iterable, but it is not an iterator.
>```iter("HELLO")``` returns an iterator

Example and explanation:
```py
for char in "Mauro"
```
A dunder built in in the _for loop_ calls ```iter()``` on "Mauro" turning that string into an iterator which then de _for loop_ keeps calling the ```next()``` method over and over until it hits the end where we dont see the StopIteration error due to an _for loop_ interception by using ```try``` & ```except``` block


#### _Iterable_


*An __Iterable__ is an object which will return an Iterator when ```iter()``` is called on it.*

i.e.: 
>```iter("HELLO")``` returns an iterator



###### next()

When ```next()``` is called on an iterator, the iterator returns the next item. It keeps doing so until it raises a ```StopIteration error```


```py
it = iter("Mauro")
print(next(it)) # M
print(next(it)) # a
print(next(it)) # u
print(next(it)) # r
print(next(it)) # o
print(next(it)) # StopIteration error
```

**Custom _for loop_**

```py
def my_for(iterable, func):
    iterator = iter(iterable)
    while True:
        try:
            thing = next(iterator)
        except StopIteration:
            break
        else:
            func(thing)
        
def square(x):
    print(x*x)

my_for("lol", print)
# l
# o
# l
my_for([1,2,3,4,5], square)
# 1
# 4
# 9
# 16
# 25

```

**Custom iterator that mocks range() function**

```py
class Counter:
    def __init__(self, low, high):
        self.current = low
        self.high = high

    def __iter__(self):
        return self

    def __next__(self):
        if self.current < self.high:
            num = self.current
            self.current += 1
            return num
        raise StopIteration

for x in Counter(50,70):
    print(x)
```

#### Generators

[Clear overview on _generators_(video)](https://www.youtube.com/watch?v=bD05uGo_sVI)
[Intro to Generators - Colt Steele (video)](https://www.udemy.com/course/the-modern-python3-bootcamp/learn/lecture/7991124#content)
[Difference btw Generators and Iterators - StackOverFlow](https://stackoverflow.com/questions/2776829/difference-between-pythons-generators-and-iterators)

Simply speaking, a generator is a function that returns an object (iterator) which we can iterate over (one value at a time).
It is fairly simple to create a generator in Python. It is as easy as defining a normal function with ```yield``` statement instead of a ```return``` statement.
The difference is that, while a ```return``` *statement terminates a function entirely*, ```yield``` *statement pauses the function saving all its states and later continues from there on successive calls*.
One interesting thing to note is that **the value of variable is remembered between each call**.
Unlike normal functions, **the local variables are not destroyed when the function yields. Furthermore, the generator object can be iterated only once. _This is because generators don't hold the entire result in memory_**. Iterators don’t compute the value of each item when instantiated. They only compute it when you ask for it. This is known as lazy evaluation.
One final thing to note is that we can use generators with ```for``` loops directly. This is because, a ```for``` loop takes an iterator and iterates over it using next() function. It automatically ends when ```StopIteration``` is raised.


* Generators are iterators

* Generators can be created with generator functions

* Generator functions use the ```yield``` keyword

* Generators can be created with generator expressions



###### Functions vs Generator Functions

**Functions**

* Uses ```return```	

* Returns once

* When invoked, returns the ```return value```


**Generator Functions**

* Uses ```yield```

* Can ```yield``` multiple times

* When invoked, returns a ```generator```


```py
def count_up_to(max):
    count = 1
    while count <= max:
        yield count
        count += 1
```

#### Exhausting a Generator

* Calling ```next()``` on a generator with nothing left to yield will throw a ```StopIteration error```

* When we loop over a generator, the loop will stop before the ```StopIteration error``` gets thrown


#### Generator Expressions

* You can also create generators from _generator expressions_

* Generator expressions look a lot like list comprehensions but Generator expressions use ```()``` instead of ```[]```
```py
(name[0] == "C" for name in names) # <generator object <genexpr> at 0x005F2FB0>
```

```py
def sum_of_nums():
    total = 0
    num = 1
    while True:
        total += num
        yield total
        num += 1

s = sum_of_nums() # another generator!
#buckle infinito
```

#### Generators Pro's:

1. Lazy evaluation (calculation on demanda)
2. Only compute values as needed
3. Can help improve performance of your code

____

# Decorators

#### Introduction to Decorators

A decorator takes in a function, adds some functionality and returns it. Functions that take other functions as arguments are also called **higher order functions**. Furthermore, a function can return another function. Functions and methods are called callable as they can be called.

In fact, any object which implements the special method ```__call__()``` is termed callable. So, in the most basic sense, a decorator is a callable that returns a callable.

```py
def make_pretty(func):
    def inner():
        print("I got decorated")
        func()
    return inner

def ordinary():
    print("I am ordinary")
```

When you run the following codes in shell,

```py
ordinary()
I am ordinary

# let's decorate this ordinary function
pretty = make_pretty(ordinary)
pretty()
# I got decorated
# I am ordinary
```
In the example shown above, ```make_pretty()``` is a decorator. In the assignment step.

```py
pretty = make_pretty(ordinary)
```

The function ```ordinary()``` got decorated and the returned function was given the name pretty.

We can see that the decorator function added some new functionality to the original function. This is similar to packing a gift. **The decorator acts as a wrapper.** The nature of the object that got decorated (actual gift inside) does not alter. But now, it looks pretty (since it got decorated).

Generally, we decorate a function and reassign it as,

```py
ordinary = make_pretty(ordinary).
```
This is a common construct and for this reason, Python has a syntax to simplify this.

We can use the ```@``` symbol along with the name of the decorator function and place it above the definition of the function to be decorated. For example,


```py
@make_pretty
def ordinary():
    print("I am ordinary")

is equivalent to

def ordinary():
    print("I am ordinary")
ordinary = make_pretty(ordinary)
```

This is just a syntactic sugar to implement decorators.


The syntax of,

```py
@star
@percent
def printer(msg):
    print(msg)
```

is equivalent to

```py
def printer(msg):
    print(msg)
printer = star(percent(printer))
```

The order in which we chain decorators matter. If we had reversed the order as,

```py
@percent
@star
def printer(msg):
    print(msg)
```

The execution would take place as,

```py
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
******************************
Hello
******************************
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```

____

[**long but clear** explanation on decorators](https://stackoverflow.com/questions/739654/how-to-make-a-chain-of-function-decorators/1594484)

____


* **High order functions** are those that either returns another function from inside or accepts another/s function/s as an argument

```py
def sum(num, func):
    total = 0
    for n in range(1, num+1):
        total += func(n)
    return total

def square(x):
    return x*x    

def cube(x):
    return x*x*x

suma = sum(10, square) # 285
suma2 = sum(10, cube) # 3025
```

* Decorators are examples of higher order functions

* Decorators are functions that wrap other functions and enhance their behavior

* We can return functions from other functions 

```py
from random import choice

def make_laugh_func():

    def get_laugh():
        l = choice(["jajaja", "lol", "jejejeje", "hohohoho"])
        return l

    return get_laugh

laugh = make_laugh_func()
print(laugh())
```

######About the () above

>If you assign a function reference to a variable, then that variable will point to a function and you can add parentheses to call/execute it like a normal function. Functions in Python are also objects and they can be assigned to variables.

>When you want to execute the function, then you add the parentheses **()** to call/invoke it. In this scenario, we are creating a function (**make_laugh_func**) that returns an inner function (**get_laugh**).

>When returning the inner **get_laugh** function from the outer **make_laugh_func**, we don't want to call it immediately at that point, and therefore we don't add parentheses to return **get_laugh**

>That allows us to return the **get_laugh** function reference from **make_laugh_func**, which we can then call at a later point.

>Then, we call the **make_laugh_func** here and save its return value to the laugh variable: ```laugh = make_laugh_func()```

>That will store the return **get_laugh** function reference to the laugh variable (but not call the inner function immediately). Then, later we can add **()** to the laugh variable in order to call the **get_laugh** function which was saved to it: ```laugh()```

>So, adding parentheses depends if you want to call and execute the function immediately, or if you are just referencing it so you can call it at a later point.


```py
from random import choice

def make_laugh_at_func(person):

    def get_laugh():
        laugh = choice(["jajaja", "lol", "jejejeje", "hohohoho"])
        return f"{laugh} {person} "

    return get_laugh

laugh_at = make_laugh_at_func("Dora")
print(laugh_at())
```


```py
def be_polite(fn):
    def wrapper():
        print("What a pleasure to meet you!")
        fn()
        print("Have a great day!")
    return wrapper

def greet():
    print("My name is Colt.")

wrapped_greet = be_polite(greet)

# What a pleasure to meet you!
# My name is Colt.
# Have a great day!

```

* Decorators have their own syntax, using **"@"** **(syntactic sugar)**

```py
def be_polite(fn):
    def wrapper():
        print("What a pleasure to meet you!")
        fn()
        print("Have a great day!")
    return wrapper

@be_polite
def greet():
    print("My name is Matt.")

# we don't need to set 
# greet = be_polite(greet)
# we just call greet()

greet()
```

#### Functions with different signatures

```py
def shout(fn):
    def wrapper(name):
        return fn(name).upper()
    return wrapper

@shout
def greet(name):
    return f"Hi, I'm {name}."

@shout
def order(main, side):
    return f"Hi, I'd like the {main}, with a side of {side}, please."
```

Won't work because ```wrapper()``` takes only one argument and two are given
```py
@shout
def order(main, side)
```



#### Standard Decorator pattern

```py
def my_decorator(fn):
    def wrapper(*args, **kwargs):
        # do some stuff with fn(*args, **kwargs)
        pass
    return wrapper
```

#### Preserving metadata

In this example, if you try to acces add.__name__ and add.__doc__ (metadata) directly and from outside the decorator, you won't be able to although you will if the wrapper is called. 

```py
def log_function_data(fn):
    """I AM WRAPPER FUNCTION""" 
    def wrapper(*args, **kwargs):
        print(f"you are about to call {fn.__name__}")
        print(f"Here's the documentation: {fn.__doc__}")
        return fn(*args, **kwargs)
    return wrapper

@log_function_data
def add(x,y):
    '''Adds two numbers together.'''
    return x + y;
```

This shows documentation
```py
print(add(10,30))
# 'you are about to call add'
# 'Here's the documentation: Adds two numbers together.'
# 40
```

This doesn't show documentation

```py
add.__doc__
add.__name__
help(add)

# wrapper(*args, **kwargs)
#    I AM WRAPPER FUNCTION
```

####Decorator pattern for preserving metadata

from _functools_ import _wrap_: **wraps preserves a function's metadata when it is decorated**
We **@wraps** right before our _wrapper_ function
It makes sure that all the attributes in the function that we are decorating aren't lost by decorator.  

```py
from functools import wraps
# wraps preserves a function's metadata
# when it is decorated

def my_decorator(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        # do some stuff with fn(*args, **kwargs)
        pass
    return wrapper
```

####Building a speed-test decorator (benchmarking)

```py
from functools import wraps
from time import time

def speed_test(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        start_time = time()
        result = fn(*args, **kwargs)
        end_time = time()
        print (f"Time Elapsed: {end_time - start_time}")
        return result
    return wrapper
@speed_test
def multiply(x):
    return (num*num for num in x)

@speed_test
def multiply(x):
    return [num*num for num in x]
```

More examples

```py
from functools import wraps
def show_args(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        args = tuple(args)
        kwargs = dict(kwargs)
        print("Here are the args: {}".format(args))
        print("Here are the kwargs: {}".format(kwargs))
        fn(*args, **kwargs)
        return fn(*args, **kwargs)
    return wrapper
```

#### Decorators to enforce certain restrictions on arguments 

For example: making a decorator that prevented a function from being called with any **kwargs** or any numerical arguments, or else.

```py
from functools import wraps

def ensure_no_kwargs(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        if kwargs:
            raise ValueError ("No kwargs allowed")
        return fn(*args, **kwargs)
    return wrapper

@ensure_no_kwargs
def greet(name):
    print (f"hi my dear friend {name}")

greet(name="jose") # ValueError
```

```py
from functools import wraps

def ensure_fewer_than_three_args(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        if len(args) < 3:
            return fn(*args, **kwargs)
        return "Too many arguments!"
    return wrapper


@ensure_fewer_than_three_args
def add_all(*nums):
    return sum(nums)

print(add_all()) # 0
print(add_all(1)) # 1
print(add_all(1,2)) # 3
print(add_all(1,2,3)) # "Too many arguments!"
print(add_all(1,2,3,4,5,6)) # "Too many arguments!"
```
other one!

```py
from functools import wraps

def only_ints(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        evaluation = all([isinstance(num, int) for num in args])
        if evaluation:
            return fn(*args, **kwargs)
        return "Please only invoke with integers"
    return wrapper

def integers(*args):
    print(all([isinstance(num, int) for num in args]))
```

___


or

___


```py
from functools import wraps
 
def only_ints(fn):
    @wraps(fn)
    def inner(*args, **kwargs):
        if any([arg for arg in args if type(arg) != int]):
            return "Please only invoke with integers."
        return fn(*args, **kwargs)
    return inner


#print(integers(1,2,3,4,5))
integers('1',2,3,4,5)
```

and... One more!


```py
'''
@ensure_authorized
def show_secrets(*args, **kwargs):
    return "Shh! Don't tell anybody!"

show_secrets(role="admin") # "Shh! Don't tell anybody!"
show_secrets(role="nobody") # "Unauthorized"
show_secrets(a="b") # "Unauthorized"
'''

from functools import wraps

def ensure_authorized(fn):
    @wraps(fn)
    def wrapper(*args,**kwargs):
        if kwargs == {'role': 'admin'}:
            return fn(*args, **kwargs)
        return "Unauthorized"
    return wrapper
```



#### Decorators with arguments




```py
def ensure_first_arg_is(val):
    def inner(fn):
        @wraps(fn)
        def wrapper(*args, **kwargs):
            if args and args[0] != val:
                return f"Invalid! First argument must be {val}"
            return fn(*args, **kwargs)
        return wrapper
    return inner
```


```py
@ensure_first_arg_is("burrito")
def fav_foods(*foods):
    print(foods)

fav_foods("burrito", "ice cream") 
  # ('burrito', 'ice cream')
fav_foods("ice cream", "burrito")
  # 'Invalid! First argument must be burrito'

@ensure_first_arg_is(10)
def add_to_ten(num1, num2):
    return num1 + num2

add_to_ten(10, 12) # 12
add_to_ten(1, 2) 
  # 'Invalid! First argument must be 10'
```

Some more!

```py
def enforce(*types):
    def decorator(f):
        def new_func(*args, **kwargs):
            #convert args into something mutable   
            newargs = []        
            for (a, t) in zip(args, types):
               newargs.append( t(a)) #feel free to have more elaborated convertion
            return f(*newargs, **kwargs)
        return new_func
    return decorator

@enforce(str, int)
def repeat_msg(msg, times):
    for time in range(times):
        print(msg)

@enforce(float, float)
def divide(a,b):
    print(a/b)
# repeat_msg("hello", '5')
divide('1', '4')

```


####Why Use Decorators?

* Removing code duplication across functions

* More easily perform function analytics/logging

* Exit out of a function early if certain conditions aren't met



#Testing

####Why testing?

* Reduce bugs in existing code

* Ensure bugs that are fixed stay fixed

* Ensure that new features don't break old ones

* ___Ensure that cleaning up code doesn't introduce new bugs___

* Makes development more fun!


## Test Driven Development (TDD)


Testing is the idea of writing code that tests your other code. TDD consists on:

#### Steps

1. Development begins by writing tests

2. Once tests are written, write code to make tests pass

3. Once tests pass, a feature is considered complete


#### Red, Green, Refactor (TDD mantra)

1. **Red**: Write a test that fails

2. **Green**: Write the minimal amount of code necessary to make the test pass

3. **Refactor**: Clean up the code, while ensuring that tests still pass




#### Assertions

**Disclaimer:** Assertions are kind of an "old" way to test codes.  

_Assertions are simply **boolean expressions** that checks if the conditions return true or not. If it is true, the program does nothing and move to the next line of code. However, if it's false, the program stops and throws an error. It is also a debugging tool as it brings the program on halt as soon as any error is occurred and shows on which point of the program error has occurred._

######Syntax
```py
assert <condition>,<error message>
```

* We can make simple assertions with the ```assert``` keyword

* ```assert``` accepts an expression

* Returns ```None``` if the expression is truthy

* Raises an ```AssertionError``` if the expression is falsy

* Accepts an optional error message as a second argument


```py
def add_positive_numbers(x, y):
    assert x > 0 and y > 0, "Both numbers must be positive!"
    return x + y

add_positive_numbers(1, 1) # 2
add_positive_numbers(1, -1) # AssertionError: Both numbers must be positive!
```

```py

def junk_food(food):
    assert food in ["ice cream", 
    "candy", 
    "fries", 
    "burger", 
    "pizza", 
    "fried butter"
    ], "Food must be junk food!"
    return "Sho taeeshty"

```


#### Assertion Warning

If a Python file is run with the ```-O flag``` (optimized mode), assertions will not be evaluated!

Ej.: in console: ```python -O prueba.py```

>**python -O does the following currently**:

> * completely ignores ```asserts```

> * sets the special builtin name ```__debug__``` to False (which by default is ```True```)

>and when called as python ```-OO```

> * removes docstrings from the code



```py
# Don't write code like this!

def do_something_bad(user):
    assert user.is_admin, "Only admins can do bad things!"
    destroy_a_bunch_of_stuff()
    return "Mua ha ha ha!"
```


#### Doctests

* __Pros__:

    * We can write tests for functions inside of the docstring

* __Downside__:
    
    * Write code that looks like it's inside of a REPL. Any missed spaced or other detail, might raise up an unexpected error.


```py
def add(x, y):
    """add together x and y

    >>> add(1, 2)
    3

    >>> add(8, "hi")
    Traceback (most recent call last):
        ...
    TypeError: unsupported operand type(s) for +: 'int' and 'str'
    """
```

Run these tests with:

python3 -m doctest -v YOUR_FILE_NAME.py
Test should fail at first - remember "Red, Green, Refactor"


#### Issues with doctests

* Syntax is a little strange

* Clutters up our function code

* Lacks many features of larger testing tools

* Tests can be brittle


```py
def add(a, b):
    """
    >>> add(2, 3)
    5
    >>> add(100,200)
    300
    """
    return a + b

def double(values):
    """ double the values in a list

    >>> double([1,2,3,4])
    [2, 4, 6, 8]

    >>> double([])
    []

    >>> double(['a', 'b', 'c'])
    ['aa', 'bb', 'cc']

    >>> double([True, None])
    Traceback (most recent call last):
        ...
    TypeError: unsupported operand type(s) for *: 'int' and 'NoneType'
    """
    return [2 * element for element in values]

# Doctests can only compare to single quoted strings    <<<<<<<<<<<<<<<<<<<<<<<<
def say_hi():
    """
    >>> say_hi()
    "hi"
    """
    return "hi"

# Watch out for whitespace!                             <<<<<<<<<<<<<<<<<<<<<<<<
# (There's a trailing space on line 42)                 <<<<<<<<<<<<<<<<<<<<<<<<
def true_that():
    """
    >>> true_that()
    True 
    """
    return True

# Order of keys in dicts matters in Doctests            <<<<<<<<<<<<<<<<<<<<<<<<
def make_dict(keys):
    """
    >>> make_dict(['a','b'])
    {'b': True, 'a': True}
    """
    return {key: True for key in keys}
```


# Unit test

[```Unittest```Python documentation here](https://docs.python.org/3/library/unittest.html)


Is the idea of testing small pieces components of your code. Is a concept that comes from the outside; not from Python strictly.


Most popular and easy to use testing method. 

* Test smallest parts of an application in isolation (e.g. units)

* Good candidates for unit testing: individual classes, modules, or functions

* Bad candidates for unit testing: an entire application, dependencies across several classes or modules

#### ```unittest```

Python comes with a built-in module called ```unittest```. You can write unit tests encapsulated as classes that inherit from ```unittest.TestCase```. This inheritance gives you access to many assertion helpers that let you test the behavior of your functions. 

You can run tests by calling ```unittest.main()```

```py
def eat(food, is_healthy):
    pass

def nap(num_hours):
    pass
```

**test**

```py
import unittest
from activities import eat, nap

class ActivityTests(unittest.TestCase):
    pass

if __name__ == "__main__":
    unittest.main()
```


**Commenting tests**

_To see comments, run:_

```python NAME_OF_TEST_FILE.py -v```

```py
class SomeTests(unittest.TestCase):
    def test_first(self):
        """testing a thing"""
        self.assertEqual(thing(), "something")

    def test_second(self):
        """testing another thing"""
        self.assertEqual(another_thing(), "something else")
```


####Type of Assertions

```py
self.assertEqual(x, y)
self.assertNotEqual(x, y)
self.assertTrue(x)
self.assertFalse(x)
self.assertIsNone(x)
self.assertIsNotNone(x)
self.assertIn(x, y)
self.assertNotIn(x, y)
```

#### Testing for errors

```py
class SomeTests(unittest.TestCase):
    def testing_for_error(self):
        """testing for an error"""
        with self.assertRaises(IndexError):
            l = [1,2,3]
            l[100]
```

## Before and After Hooks

####```setUp``` and ```tearDown```

* For larger applications, you may want similar application state before running tests

* setUp runs before each test method

* tearDown runs after each test method

* Common use cases: adding/removing data from a test database, creating instances of a class


```py
class SomeTests(unittest.TestCase):

    def setUp(self):
        # do setup here
        pass

    def test_first(self):
        # setUp runs before
        # tearDown runs after
        pass

    def test_second(self):
        # setUp runs before
        # tearDown runs after
        pass

    def tearDown(self):
        # do teardown here
        pass
```



# File I/O - File Input/Output


## Reading files

* You can read a file with the ```open``` function

* open returns a file object to you

* You can read a file object with the ```read``` method


**story.txt**

```This short story is really short.```

**reading_files.py**

```py
file = open("story.txt")
file.read()
```

#### Cursor movement

Python reads files by using a cursor. This is like the cursor you see when you're typing. After a file is read, the cursor is at the end. To move the cursor, use the ```seek``` method. 

```py
file = open('archivo1.txt')
reading = file.read()
print(reading)
file.seek(0) # moves the cursor to the begining of the file
```

* To read only part of a file, pass a number of characters into read, or use ```readline()```

```py
file = open('archivo1.txt')
print(reading)
file.readline() # reads the first line and moves de cursor to the end of that line
```


* To get a list of all lines, use ```readlines()```. This methods preserve lines as separate lines and puts them in a list. Finally, moves the cursor to the end.


```py
file = open('archivo1.txt')
print(reading)
file.readlines()
# ['Archivo 1\n', 'Mauro Consolani\n', 'Y ahora esto se agrega\n', 'y esto?\n', 'Joya.. pero que pasa con esto?']
``` 


## Closing a file

You can close a file with the ```close method```. You can check if a file is closed with the closed attribute. **Once closed, a file can't be read again**. _Always close files - it frees up system resources!_

```py
file = open('archivo1.txt')
reading = file.readlines()
print(reading)
file.seek(0) # moves to the begining 
file.close() # Closes de file
print(file.closed) #Checks if file is closed
# True
```

#### ```with``` Blocks

Lets check the ```with``` syntax to work with files. 

**Option 1**


```py
file = open("story.txt")
file.read()
file.close()

file.closed # True
```

**Option 2**

```py
with open("story.txt") as file:
    file.read()

file.closed # True
```

>```as file```the "file" could be called what ever we want.
> the ```with``` is also responsible for **closing the file automatically** after it's been use. We don't have to close it manually anymore. 

```py
with open ('archivo1.txt') as archivo1:
    content = archivo1.readlines()
    archivo1.seek(0)
    print(content) 
    print(archivo1.closed) # False

print(archivo1.closed) # Trues
```

As you see, when you work out of the ```with``` block, the file is closed. This happens because ```with``` has a built in method at the end (```.__exit__```) which exits the ```with``` block. Conclusion: must work the files alway inside the ```with``` block.  


## Writing to Text Files

You can also use ```open``` to write to a file. Need to specify the "w" flag as the second argument

```py
with open("haiku.txt", "w") as file:
    file.write("Writing files is great\n")
    file.write("Here's another line of text\n")
    file.write("Closing now, goodbye!")
``` 

**_IMPORTANT:_**

* If you open the file again to write, the original contents will be deleted!

* If you reference a file which doesn't exist in writing mode, it will create a new file with the referenced name. 

## Modes for opening files

1. ***r*** - Read a file (no writing) - this is the default

2. ***w*** - Write to a file (previous contents removed)

3. ***a*** - Append to a file (previous contents not removed)
    * It adds at the end of the file

4. ***r+*** - Read and write to a file (writing based on cursor)
    * It start from where the cursor is
    * If there is something after the cursor, it will be overwritten
    * It only works with an existing file. If the file doesn't exist, it just shows an error but doesn't create one. 

```py
# r+ read and write
with open("haiku.txt", "r+") as file:
    file.write(":)")
    file.seek(10)
    file.write(":(")

# r+ will not create a file if it doesn't exist
with open("hello.txt", "a") as file:
    file.write("HELLO!!!")
```

```py
def copy(file_name, new_name):
    with open(file_name) as first_file:
        data = first_file.read()
    with open(new_name, 'w') as second_file:
        second_file.write(data)
    return
```

##Truncating Files

```file.truncate``` - removes all text starting from the current cursor position


## Reading CSV Files

CSV files are a common file format for tabular data. We can read CSV files just like other text files. Python has a built-in CSV module to read/write CSVs more easily

**fighter.csv**

```
Name,Country,Height (in cm)
Ryu,Japan,175
Ken,USA,175
Chun-Li,China,165
Guile,USA,182
E. Honda,Japan,185
Dhalsim,India,176
Blanka,Brazil,192
Zangief,Russia,214
```

**reading_csv.py**

```py
with open("fighters.csv") as file:
    file.read() >>>>>>>>>>>>> #DON'T DO THIS#
```

#### CSV Module

1. ```reader``` - It's a generator. Allows you to iterate over rows of the CSV as lists. O sea, convierte cada fila en una lista cada una, para que luego puedas iterar sobre cada una de ellas, incluyendo los headers. 

```py
<_csv.reader object at 0x00452F30>
<class '_csv.reader'>
```
    
* Considering a **generator** is generated by ```reader```, you could use ```next()``` to skip headers when iterating.
```['Zangief', 'Russia', '214']```


```py
from csv import reader
with open("fighters.csv") as file:
    csv_reader = reader(file)
    next(csv_reader) # This skips the headers    
    for row in csv_reader:
        # each row is a list!
        print(row)
``` 

2. ```DictReader``` - lets you iterate over rows of the CSV as OrderedDicts (special Python collection). O sea, convierte cada fila en OrderedDicts. As it is a generator, you can only go over it once. 

```py
<csv.DictReader object at 0x009895B0>
<class 'csv.DictReader'>
```

* The keys are set automatically to be the headers. i.e.: ```OrderedDict([('Name', 'Ryu'), ('Country', 'Japan'), ('Height (in cm)', '175')])```


```py
from csv import DictReader
with open('fighters.csv') as file:
    data = DictReader(file)
    #next(data)
    for fighter in data:
        print(fighter['Name'])
Ryu
Ken
Chun-Li
Guile
E. Honda
Dhalsim
Blanka
Zangief
```


3. Keys are determined by the header row


4. An OrderedDict is like a dictionary, but it remembers the order in which keys were inserted


**reader**

```py
from csv import reader
with open("fighters.csv") as file:
    csv_reader = reader(file)
    for row in csv_reader:
        # each row is a list!
        print(row) 
```

```
['Name', 'Country', 'Height (in cm)']
['Ryu', 'Japan', '175']
['Ken', 'USA', '175']
['Chun-Li', 'China', '165']
['Guile', 'USA', '182']
['E. Honda', 'Japan', '185']
['Dhalsim', 'India', '176']
['Blanka', 'Brazil', '192']
['Zangief', 'Russia', '214']
```

**DictReader**

```py
from csv import DictReader
with open("fighters.csv") as file:
    csv_reader = DictReader(file)
    for row in csv_reader:
        # Each row is an OrderedDict!
        print(row['Name']) #Use keys to access data
```

```
OrderedDict([('Name', 'Ryu'), ('Country', 'Japan'), ('Height (in cm)', '175')])
OrderedDict([('Name', 'Ken'), ('Country', 'USA'), ('Height (in cm)', '175')])
OrderedDict([('Name', 'Chun-Li'), ('Country', 'China'), ('Height (in cm)', '165')])
OrderedDict([('Name', 'Guile'), ('Country', 'USA'), ('Height (in cm)', '182')])
OrderedDict([('Name', 'E. Honda'), ('Country', 'Japan'), ('Height (in cm)', '185')])
OrderedDict([('Name', 'Dhalsim'), ('Country', 'India'), ('Height (in cm)', '176')])
OrderedDict([('Name', 'Blanka'), ('Country', 'Brazil'), ('Height (in cm)', '192')])
OrderedDict([('Name', 'Zangief'), ('Country', 'Russia'), ('Height (in cm)', '214')])
```


####Other Delimiters

Readers accept a delimiter kwarg in case your data isn't separated by commas. You can use files that aren't actually separated by comas as long as they are separated by the **same character**. That character is known as the **delimiter** 


```py
from csv import reader
with open("example.csv") as file:
    csv_reader = reader(file, delimiter="|")
    for row in csv_reader:
        # each row is a list!
        print(row) 
```

##Writing CSV files

#### Using Lists

1. ```writer``` - creates a writer object for writing to CSV
2. ```writerow``` - method on a writer to write a row to the CSV

```py
from csv import writer
with open("fighters.csv", "w") as file:
    csv_writer = writer(file)
    csv_writer.writerow(["Character", "Move"])
    csv_writer.writerow(["Ryu", "Hadouken"])
```

```py
from csv import reader, writer
# using nested with statements
with open('fighters.csv') as file:
    csv_reader = reader(file) #data never converted to list
    with open('screaming_fighters.csv', "w") as file:
        csv_writer = writer(file)
        for fighter in csv_reader:
            csv_writer.writerow([s.upper() for s in fighter])
```



#### Using Dictionaries

1. ```DictWriter``` - creates a writer object for writing using dictionaries
2. ```fieldnames``` - kwarg for the DictWriter specifying headers
3. ```writeheader``` - method on a writer to write header row 
4. ```writerow``` - method on a writer to write a row based on a dictionary


```py
from csv import DictWriter
with open("example.csv", "w") as file:
    headers = ["Character", "Move"]
    csv_writer = DictWriter(file, fieldnames=headers)
    csv_writer.writeheader()
    csv_writer.writerow({
        "Character": "Ryu", 
        "Move": "Hadouken"
    })
```

[Keeping track when iterating - Everything on enumarate](https://www.geeksforgeeks.org/enumerate-in-python/)



# Pickling

[Pickling by Colt Steele](https://www.udemy.com/course/the-modern-python3-bootcamp/learn/lecture/9023194#questions)
[Pickiling by GeeksforGeeks](https://www.geeksforgeeks.org/understanding-python-pickling-example/)


Significa agarrar algun objeto de Python y ponerlo en "vinagre" para que se conserve ahi por un buen tiempo. Python serializa la data, lo convierte en un byte stream y despues lo podemos unpickle y sacarlo de ese archivo y ponerlo donde sea que estaba antes.

```pickle``` module is used for serializing and de-serializing a Python object structure. Any object in Python can be pickled so that it can be saved on disk. What pickle does is that it “serializes” the object first before writing it to file. **Pickling is a way to convert a python object (list, dict, etc.) into a character stream.** The idea is that this character stream contains all the information necessary to reconstruct the object in another python script. 

It's useful to store Python data somewhere until you need to retrieve it again for it's use. 
On the other hand, it's not a good way to store data if you need it while it's being stored in another format because binary is not easy to read or catch for other languages or whatever. 


**Syntax**

_To Pickle_

```py
pickle.dump(obj, file, protocol=None, *, fix_imports=True, buffer_callback=None)
```

Ej.: 
```py
with open("pets.pickle", "wb") as file:
    pickle.dump(blue, file)
```

We use ***"wb"*** flag because we are **writing binary**

Write the pickled representation of the object ```obj``` to the open file object ```file```. This is equivalent to ```Pickler(file, protocol).dump(obj)```.

_To Unpickle_

```py
pickle.load(file, *, fix_imports=True, encoding="ASCII", errors="strict", buffers=None)
```

Ej.: 

```py
with open("pets.pickle", "rb") as file:
    zombie_blue = pickle.load(file)
```

We use ***"rb"*** flag because we are **reading binary**

Read the pickled representation of an object from the open file object ```file``` and return the reconstituted object hierarchy specified therein. This is equivalent to ```Unpickler(file).load()```.

The protocol version of the pickle is detected automatically, so no ```protocol``` argument is needed. Bytes past the pickled representation of the object are ignored.


```py

import pickle
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species

    def __repr__(self):
        return f"{self.name} is a {self.species}"

    def make_sound(self, sound):
        print(f"this animal says {sound}")


class Cat(Animal):
    def __init__(self, name, breed, toy):
        super().__init__(name, species="Cat") # Call init on parent class
        self.breed = breed
        self.toy = toy

    def play(self):
        print(f"{self.name} plays with {self.toy}")


blue = Cat("Blue", "Scottish Fold", "String")

# To pickle an object:
with open("pets.pickle", "wb") as file:
    pickle.dump(blue, file)

#To unpickle something:
with open("pets.pickle", "rb") as file:
    zombie_blue = pickle.load(file)
    print(zombie_blue)
    print(zombie_blue.play())
```


**Zarko about pickling:**
Pickling is a way to convert a Python object (list, dict, etc.) into a character stream. The idea is that this character stream contains all the information necessary to reconstruct the object in another Python script. 

See the following thread to find some of the most commonly mentioned use-cases for pickling: https://stackoverflow.com/a/3439921 (I found saving the gaming profiles/saved games especially interesting)



## JSON Pickling

[JSON pickle](https://jsonpickle.github.io/)

_Allows us to take Python object and turn it into a JSON:_

```py
j = json.dumps(['foo', {'bar': ('baz', None, 1.0, 2)}])
```
This formats a Python object into a STRING of JSON. This could be consumed by other developers. 

**One step forward:**
jsonpickle is a Python library for serialization and deserialization of complex Python objects to and from JSON. The standard Python libraries for encoding Python into JSON, such as the stdlib’s json, simplejson, and demjson, can only handle Python primitives that have a direct JSON equivalent (e.g. dicts, lists, strings, ints, etc.). jsonpickle builds on top of these libraries and allows more complex data structures to be serialized to JSON. jsonpickle is highly configurable and extendable–allowing the user to choose the JSON backend and add additional backends.


**Pickling with _jsonpickle_ module**

```py
import jsonpickle

class Cat:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

c = Cat("Charles", "Tabby")

# To JSONPICKLE 'c' the cat:
with open("cat.json", "w") as file:
    frozen = jsonpickle.encode(c)
    file.write(frozen)

# To bring back 'c' the cat using JSONPICKLE
with open("cat.json", "r") as file:
    contents = file.read()
    unfrozen = jsonpickle.decode(contents)
    print(unfrozen)
```



# Web Scrapping


Web scraping involves programmatically grabbing data from a web page. Consists on three steps: 

1. Download
2. Extract data
3. Profit: okay...more like, do something with data


#### Why scrape?

* There's data on a site that you want to store or analyze

* You can't get by other means (e.g. an API)

* You want to programmatically grab the data (instead of lots of manual copying/pasting)

>**Is it...ok?**

>Some websites don't want people scraping them

>Best practice: consult the ```robots.txt``` file

>If making many requests, time them out

>If you're too aggressive, your IP can be blocked

____


#### HTML/CSS Crash Course

**HTML:** HyperText Markup Language 
Helps to encode a msg to send it de forma homogenea de un lugar a otro.

Si guardas un archivo en formato .html sin nada y luego entras y apretas html + tab, sale esto:
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>

</body>
</html>


**CSS:** Cascading Style Sheet
Allows us to add style to html. The good practice is to put the .CSS code in a different file. 

_id_ = impacts only in one element
_class_ = impact in multiple items. 

<!DOCTYPE html>
<html>
<head>
    <title>Bread Recipe</title>
</head>
<body>
    <h1>SF Sourdough Loaf</h1>
    <style type="text/css">
        h1{
            color: purple;
            background: grey;
        }
        li {
            color: red;
            font-size: 20px;
        }
        #first {
            color: blue;
        }
        .green {
            color: teal;
        }
    </style>
    <em id="first">Written by Colt Steele</em>
    <h3>Ingredients</h3>
    <ul>
        <li class = "green">Ing. 1</li>
        <li class = "green">Ing. 2</li>
        <li>Ing. 3</li>


    </ul>
</body>
</html>


#### codigo HTML sobre el que se basó la practica

html = """
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>First HTML Page</title>
</head>
<body>
  <div id="first">
    <h3 data-example="yes">hi</h3>
    <p>more text.</p>
  </div>
  <ol>
    <li class="special">This list item is special.</li>
    <li class="special">This list item is also special.</li>
    <li>This list item is not special.</li>
  </ol>
  <div data-example="yes">bye</div>
</body>
</html>
"""


### Introduction to Beautiful Soup

[bs4 documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

To extract data from HTML, we'll use ```Beautiful Soup```. Install it with pip. Beautiful Soup lets us navigate through HTML with Python. Beautiful Soup does NOT download HTML - for this, we need the requests module!


#### Parsing and Navigating HTML

```py
BeautifulSoup(html_string, "html.parser") - parse HTML. Once parsed, there are several ways to navigate:
```

* By Tag Name
* Using ```find``` - returns **one** matching tag
* Using ```find_all``` - returns a **list** of matching tags

```py
soup.find_all(class_="special")

# [<li class="special">This list item is special.</li>, <li class="special">This list item is also special.</li>]
```


Retrieves every element that has the attribute "data-example" set to "yes"

```py
soup.find_all(attrs={"data-example": "yes"})

# [<h3 data-example="yes">hi</h3>, <div data-example="yes">bye</div>]
```


#### Navigating with CSS Selectors

Allows us to navigate based of CSS selectors

```select``` - returns a **list** of elements matching a CSS selector

```py
soup.select("[data-example]")
```

```py
soup.select("[data-example]")[0] # ---> access to 1st. element in list
```

**Selector Cheatsheet**

* Select **by id** of foo: #foo ```soup.select("#foo")[0]```

* Select **by class** of bar: .bar ```soup.select(".bar")```

* Select **children**: div > p

* Select **descendents**: div p

* Select **attributes**: [] ```soup.select("[data-baz]")```

It’s very useful to search for a tag that has a certain CSS class, but the name of the CSS attribute, “class”, is a reserved word in Python. Using class as a keyword argument will give you a syntax error. As of Beautiful Soup 4.1.2, you can search by CSS class using the keyword argument ```class_```

```py
# find an element with an id of foo
soup.find(id="foo")
soup.select("#foo")[0]

# find all elements with a class of bar
# careful! "class" is a reserved word in Python
soup.find_all(class_="bar")
soup.select(".bar")

# find all elements with a data
# attribute of "baz"
# using the general attrs kwarg
soup.find_all(attrs={"data-baz": True})
soup.select("[data-baz]")
```

#### Accessing Data in Elements

1. ```.get_text()``` - access the inner text in an element

```py
soup = BeautifulSoup(html, "html.parser")
ele = soup.select(".special")
for l in ele:
    print(ele.get_text())

# This list item is special.
# This list item is also special.
```

2. ```.name``` - (not a method) returns the name of the tag

```py
soup = BeautifulSoup(html, "html.parser")
ele = soup.select(".special")
for l in ele:
    print(l.name)
#li
#li
```


3. ```attrs``` - dictionary containing **attributes** on each item. 

```py
soup = BeautifulSoup(html, "html.parser")
ele = soup.select(".special")
for l in ele:
    print(l.attrs)
# {'class': ['special']}
# {'class': ['special']}
```

4. You can also access attribute values using brackets!

Could also do:

```py
soup = BeautifulSoup(html, "html.parser")
attrs = soup.find("div")["id"]
print(attrs)
# First
due to ->>>>  <div id="first">
```
**It finds the first "<div>" and retrieves the "id" attribute**. The [] refers to the attribute. ```<div id="first">```     



#### Navigating with Beautiful Soup

This is useful when searching for an element and can't do it straigh forward. So you pick a reference element and then search the element via tags, using attributes. Some times its harder than you would expect to select the particular things that you want, so you get close and then you navigate towards it. 

**Via Tags** using attributes

1. **parent / parents**
    * **Parent**: goes up one "layer". Gives us the tag that is enclosing the one where we are calling the ```parent```from.
    ```py
    data2 = soup.find(class_="special").parent
    # <ol>
    # <li class="special">This list item is special.</li>
    # <li class="special">This list item is also special.</li>
    # <li>This list item is not special.</li>
    # </ol>
    ```

2. **contents**
    * retrieves all the content inside the tag called
    ```py
    soup = BeautifulSoup(html, 'html.parser')
    data = soup.body.contents[1]
    print(data)
    # ['\n', <div id="first">
    # <h3 data-example="yes">hi</h3>
    # <p>more text.</p>
    # </div>, '\n', <ol>
    # <li class="special">This list item is special.</li>
    # <li class="special">This list item is also special.</li>
    # <li>This list item is not special.</li>
    # </ol>, '\n', <div data-example="yes">bye</div>, '\n']
    ```
3. **next_sibling / next_siblings**
    * **Siblings**: means they are the same level in herarchy. Ej.:
    
    ```py
    <div>Sibling</div>
        <li> sthing </li>
        <li> sthing </li>
        <li> sthing </li>
        <li> sthing </li>

    <div>Sibling</div>
        <li>something</li>
    ...

    ```

4. **previous_sibling / previous_siblings**


**Via Searching** using methods


1. **.find_parent()** / **.find_parents()**
    * Finds parent tag. 
    
    ```py
    soup = BeautifulSoup(html, 'html.parser')
    data = soup.find("h3").find_parent()
    print(data)

    # <div id="first">
    # <h3 data-example="yes">hi</h3>
    # <p>more text.</p>
    # </div>
    ```


2. **.find_next_sibling()** / **.find_next_siblings()**
    * Find the next tag located at the same herarchty level.
    i.e.: We will find the next sibling of this ```<div>``` tag
    
    ```
    <div id="first">
    <h3 data-example="yes">hi</h3>
    <p>more text.</p>
    </div>
    ```

    ```py
    soup = BeautifulSoup(html, 'html.parser')
    data = soup.find(id="first").find_next_sibling()
    print(data)
    # <ol>
    # <li class="special">This list item is special.</li>
    # <li class="special">This list item is also special.</li>
    # <li>This list item is not special.</li>
    # </ol>

    ```


3. **.find_previous_sibling()** / **.find_previous_siblings()**
    * Find previous tag existing at the same hirerachy level

    ```py
    soup = BeautifulSoup(html, 'html.parser')
    data = soup.find("ol").find_previous_sibling()
    print(data)

    # <div id="first">
    # <h3 data-example="yes">hi</h3>
    # <p>more text.</p>
    # </div>
    ```


____
If you need to navigate with some specification, you can add it in the parenthesis like. 

```py
soup = BeautifulSoup(html, 'html.parser')
data = soup.find(id="first").find_next_sibling("div")
print(data)
#<div data-example="yes">bye</div>
```

____




#### Common Issues with Web Scraping

* Gnarly HTML
* Code tightly coupled to UI
* Sanitizing data after grabbing it
* Data that isn't part of HTML, but is loaded later!


#### Other Tools for Web Scraping

* ___Scrapy:___ https://scrapy.org/

A more streamlined way to build web crawlers, which can programmatically navigate across multiple pages. Can export to many 
different file formats from the command line

* ___Selenium:___ http://www.seleniumhq.org/

Allows you to open up a browser window from your code! Often used with testing. Requires a driver for your browser of choice. Doesn't navigate through the page until all contents have loaded. 


# Scrapy

[Scrapy Documentation](https://docs.scrapy.org/en/latest/topics/spiders.html)

Framework for extracting data. It bundles together the making of HTTP requests along with the extraction of the data and writing the data to a file and it can very easly change from writing to .csv file or to .json file; It has all this functionalities built in with just a couple of lines

####Spiders

Spiders are classes which define how a certain site (or a group of sites) will be scraped, including how to perform the crawl (i.e. follow links) and how to extract structured data from their pages (i.e. scraping items). In other words, **Spiders are the place where you define the custom behaviour for crawling and parsing pages for a particular site (or, in some cases, a group of sites).**

```py
import scrapy

class BookSpider(scrapy.Spider):
    name = 'bookspider'
    start_urls = ['http://books.toscrape.com/']

    def parse(self, response):
        """this is how we want to parse the result of the request """
        for article in response.css('article.product_pod'):
            yield {
                'price': article.css(".price_color::text").extract_first(),
                'title': article.css("h3 > a::attr(title)").extract_first()
            }
            next = response.css('.next > a::attr(href)').extract_first()
            if next:
                """DISCLAIMER: this loops through all pages in the website"""
                yield response.follow(next, self.parse)
```

# RegEx - Regular Expressions

[RegEx Cheat Sheet](http://www.rexegg.com/regex-quickstart.html)

[Regular Expression Operators - Documentation](https://docs.python.org/3/library/re.html)

[Regular Expression tester](https://pythex.org/)

[RegEx Video - Colt Steele - Python Bootcamp](https://www.udemy.com/course/the-modern-python3-bootcamp/learn/lecture/9328490#questions)

[Practici RegEx](https://regexone.com/)

It's not a Python specific topyc. It's a concept that is separate from Python, but Python has an implementation where we can write and use regular expressions in our code. **They are a way of describing patterns within search strings.** It's a fancy set of sytax of special characters that we can string together to make patterns that we want to match. 

A Regular Expression (RegEx) is a sequence of characters that defines a search pattern.
For example,

```^a...s$```

The above code defines a RegEx pattern. The pattern is: any five letter string starting with a and ending with s.


#### Potential Use Cases

1. Credit Card number validating
2. Phone number validating
3. Advanced find/replace in text
4. Formatting text/output
5. Syntax highlighting

#### Specify Pattern Using RegEx

To specify regular expressions, **metacharacters** are used. Metacharacters are _characters that are interpreted in a special way by a RegEx engine_. Here's a list of metacharacters:

```[] . ^ $ * + ? {} () \ |```

1. **[]**: Square brackets specifies a set of characters you wish to match.
```[abc]```
Here, ```[abc]``` will match if the string you are trying to match contains any of the a, b or c.
You can also specify a range of characters using - inside square brackets.
```
[a-e] is the same as [abcde].
[1-4] is the same as [1234].
```


2. 

#### REGEX OUTSIDE OF PYTHON

THERE ARE A TON OF REGEX SYMBOLS. I'm just going to cover some important ones

##### Some characters

1. **\d**:  digit 0-9
2. **\w**:  letter, digit, or underscore
3. **\s**:  whitespace character
4. **\D**:  not a digit
5. **\W**:  not a word character
6. **\S**:  not a whitespace character
7. **.** :  any character except line break

##### Quantifiers

1. **+**: One or more 
2. **{3}**: Exactly x times.  {3} - 3 times
3. **{3,5}**:   Three to five times
4. **{4,}**:     Four or more times
5. **\***: Zero or more times
6. **?**: Once or none (optional)

##### Anchors and Boundaries

1. **^**: Start of string or line
2. **$**: End of string or line
3. **\b**: Word boundary


#### Using REGEX in Python

```py
#import regex module
import re

#define our phone number regex
pattern = re.compile(r'\d{3} \d{3}-\d{4}')

#search a string with our regex (finds the first match)
res = pattern.search('Call me at 415 555-4242!')

# Returns a match object
<re.Match object; span=(11, 23), match='415 555-4242'>

#This gets out the match from the match object.  
res.group()

#'415 555-4242'

#Finds all matches
res = pattern.findall('Call me at 415 555-4242 or at 310 545-2322!')

#['415 555-4242', '310 545-2322']

```

The ```r``` in ```pattern = re.compile(r'\d{3} \d{3}-\d{4}')``` stands for ```raw```. If you don't use it you would have to escape those characters or sequences as Python expects you to. Using ```r```, there is no need to escape characters. Compiling means turning the RegEx into a RegEx object; it's useful when need to reuse the code. 


If you don't compile the pattern, here is the other alternative:

```py
import re

res = re.findall(r'\d{3} \d{3}-\d{4}', 'Call me at 415 555-4242 or at 310 545-2322!')
```

```py
import re
# Returns first instance of phone number pattern:
def extract_phone(input):
    phone_regex = re.compile(r'\b\d{3} \d{3}-\d{4}\b')
    match = phone_regex.search(input)
    if match:
        return match.group()
    return None

# Returns all instances of phone number pattern in a list
def extract_all_phones(input):
    phone_regex = re.compile(r'\b\d{3} \d{3}-\d{4}\b')
    return phone_regex.findall(input)

# One way of checking if entire string is valid phone number:
# def is_valid_phone(input):
#   phone_regex = re.compile(r'^\d{3} \d{3}-\d{4}$')
#   match = phone_regex.search(input)
#   if match:
#       return True
#   return False

# Another way of doing the same thing, using the fullmatch method
# fullmatch returns a match only if the entire input string is a match. No need for ^ and $ 
def is_valid_phone(input):
    phone_regex = re.compile(r'\d{3} \d{3}-\d{4}')
    match = phone_regex.fullmatch(input)
    if match:
        return True
    return False
```

```print(match.groups())``` (with **s**) returns a tuple with all the componentes in the compiled RegEx divided by ```()```. 
Thus, you can call, ```match.group(index)``` (without **s**) to refference a specific index element.  

```match.group(0)```: returns all the elements in the tuple (anti-Pythonic index calling)
```match.group(1)```: returns all the elements in the tuple and add one to the index to iterate over the rest of the elements



```py
import re

url_regex = re.compile(r'(https?)://(www\.[A-za-z-]{2,256}\.[a-z]{2,6})([-a-zA-Z0-9@:%_\+.~#?&//=]*)')
match = url_regex.search("https://www.my-website.com/bio?data=blah&dog=yes")
print(f"Protocol: {match.group(1)}")
print(f"Domain: {match.group(2)}")
print(f"Everything Else: {match.group(3)}")
print(match.groups())
print(match.group())
```


```py
import re
# define parse_bytes below:

def parse_bytes(string):
    pattern = re.compile(r'(\b\d{8}\b)')
    lista = pattern.findall(string)
    return lista

print(parse_bytes("11010101 101 323"))
print(parse_bytes("asda"))
['11010101']
[]
```


```py
import re

def parse_date(date):
    pattern = re.compile(r'(\d\d)[.,/](\d\d)[.,/](\d\d\d\d)')
    lista = pattern.fullmatch(date)
    if lista:
        lista = list(lista.groups())
        key = ['d', 'm', 'y']
        zipper = dict(zip(key,lista))
        return zipper
    return None


print(parse_date("12,04,2012"))
print(parse_date("12.04.2012"))
print(parse_date("12/04/2012"))
```

#####Compilation Flags

[Python Doc. on REGEX for further info](https://docs.python.org/3/library/re.html)

They let you modify aspects of how regular expression work. 

The expression’s behaviour can be modified by specifying a flags value. Values can be any of the following variables, combined using bitwise OR (the \| operator).

```py
pattern = re.compile(r"""
    ^([a-z0-9_\.-]+)    #first part of email    
    @                   #single @ sign
    ([0-9a-z\.-]+)      #email provider
    \.                  #single period
    ([a-z\.]{2,6})$     #com, org, net, etc.
""", re.X | re.I) <<<<<<<<<<<<<<<<<<<
```

use ```|```to use two or more flags in the same RE


1. ***ignorecase***: ```re.IGNORECASE``` or ```re.I``` 

Perform case-insensitive matching; expressions like [A-Z] will also match lowercase letters. Full Unicode matching (such as Ü matching ü) also works unless the re.ASCII flag is used to disable non-ASCII matches. The current locale does not change the effect of this flag unless the re.LOCALE flag is also used. Corresponds to the inline flag (?i).

Note that when the Unicode patterns [a-z] or [A-Z] are used in combination with the IGNORECASE flag, they will match the 52 ASCII letters and 4 additional non-ASCII letters: ‘İ’ (U+0130, Latin capital letter I with dot above), ‘ı’ (U+0131, Latin small letter dotless i), ‘ſ’ (U+017F, Latin small letter long s) and ‘K’ (U+212A, Kelvin sign). If the ASCII flag is used, only letters ‘a’ to ‘z’ and ‘A’ to ‘Z’ are matched.


2. ***verbose*** - ```re.VERBOSE``` or ```re.X```

This flag allows you to write regular expressions that look nicer and are more readable by allowing you to visually separate logical sections of the pattern and add comments. Whitespace within the pattern is ignored, except when in a character class, or when preceded by an unescaped backslash, or within tokens like \*?, (?: or (?P<...>. When a line contains a # that is not in a character class and is not preceded by an unescaped backslash, all characters from the leftmost such # through the end of the line are ignored.

This means that the two following regular expression objects that match a decimal number are functionally equal:

```py
a = re.compile(r"""\d +  # the integral part
                   \.    # the decimal point
                   \d *  # some fractional digits""", re.X)

b = re.compile(r"\d+\.\d*")
```

```py
# Without Verbose Flag...
# pat = re.compile(r'^([a-z0-9_\.-]+)@([0-9a-z\.-]+)\.([a-z\.]{2,6})$')
import re
pattern = re.compile(r"""
    ^([a-z0-9_\.-]+)    #first part of email    
    @                   #single @ sign
    ([0-9a-z\.-]+)      #email provider
    \.                  #single period
    ([a-z\.]{2,6})$     #com, org, net, etc.
""", re.X | re.I)

match = pattern.search("ThomaS123@Yahoo.com")
print(match.group())
print(match.groups())
```

#### Substitution - Finding and replacing

###### ```RE.sub``` method

```py
re.sub(pattern, repl, string, count=0, flags=0)
```

Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string by the replacement ```repl```. If the pattern isn’t found, string is returned unchanged. ```repl``` can be a string or a function; if it is a string, any backslash escapes in it are processed. That is, ```\n``` is converted to a single newline character, ```\r``` is converted to a carriage return, and so forth. Unknown escapes of ASCII letters are reserved for future use and treated as errors. Other unknown escapes such as ```\&``` are left alone. Backreferences, such as ```\6```, are replaced with the substring matched by group 6 in the pattern. For example:

```py
>>>
>>> re.sub(r'def\s+([a-zA-Z_][a-zA-Z_0-9]*)\s*\(\s*\):',
...        r'static PyObject*\npy_\1(void)\n{',
...        'def myfunc():')
'static PyObject*\npy_myfunc(void)\n{'
```
If ```repl``` is a function, it is called for every non-overlapping occurrence of pattern. The function takes a single match object argument, and returns the replacement string. For example:

```py
def dashrepl(matchobj):
    if matchobj.group(0) == '-': return ' '
    else: return '-'

re.sub('-{1,2}', dashrepl, 'pro----gram-files')
'pro--gram files'

re.sub(r'\sAND\s', ' & ', 'Baked Beans And Spam', flags=re.IGNORECASE)
'Baked Beans & Spam'
```

The pattern may be a string or a pattern object.

The optional argument count is the maximum number of pattern occurrences to be replaced; count must be a non-negative integer. If omitted or zero, all occurrences will be replaced. Empty matches for the pattern are replaced only when not adjacent to a previous empty match, so sub('x\*', '-', 'abxd') returns '-a-b--d-'.

In string-type repl arguments, in addition to the character escapes and backreferences described above, \g<name> will use the substring matched by the group named name, as defined by the (?P<name>...) syntax. \g<number> uses the corresponding group number; \g<2> is therefore equivalent to \2, but isn’t ambiguous in a replacement such as \g<2>0. \20 would be interpreted as a reference to group 20, not a reference to group 2 followed by the literal character '0'. The backreference \g<0> substitutes in the entire substring matched by the RE.


```py
Pattern.sub(repl, string, count=0)
```

Identical to the ```sub()``` function, using the compiled pattern.

```py
import re
text = "Last night Mrs. Daisy and Mr. white murdered Ms. Chow"

pattern = re.compile(r'(Mr.|Mrs.|Ms.) ([a-z])[a-z]+', re.I)
result = pattern.sub("\g<1> \g<2>", text)
print(result)

#Last night Mrs. D and Mr. w murdered Ms. C
```

```py
import re
titles = [
    "Significant Others (1987)",
    "Tales of the City (1978)",
    "The Days of Anna Madrigal (2014)",
    "Mary Ann in Autumn (2010)",
    "Further Tales of the City (1982)",
    "Babycakes (1984)",
    "More Tales of the City (1980)",
    "Sure of You (1989)",
    "Michael Tolliver Lives (2007)"
]
titles.sort()
fixed_titles = []

pattern = re.compile(r'(?P<title>^[\w ]+) \((?P<date>\d{4})\)')
for book in titles:
    # result = pattern.sub("\g<2> - \g<1>", book)
    result = pattern.sub("\g<date> - \g<title>", book)

    fixed_titles.append(result)
fixed_titles.sort()
print(fixed_titles)
```


# SQL with Python

Using **SQLite3**

[SQLite Documentation](https://www.sqlite.org/docs.html)

**SQL**: Structured Query Language

SQL (pronounced "ess-que-el") stands for Structured Query Language. SQL is used to communicate with a database. According to ANSI (American National Standards Institute), it is the standard language for relational database management systems. SQL statements are used to perform tasks such as update data on a database, or retrieve data from a database. Some common relational database management systems that use SQL are: Oracle, Sybase, Microsoft SQL Server, Access, Ingres, etc. Although most database systems use SQL, most of them also have their own additional proprietary extensions that are usually only used on their system. However, the standard SQL commands such as "Select", "Insert", "Update", "Delete", "Create", and "Drop" can be used to accomplish almost everything that one needs to do with a database.


###### Getting ```.help```

1. ```.help``` gives you access to the SQL commands.

2. ```.table``` tells you if there is any table in the data base. Pretty much, we use SQL to store data in tables. Each table has different columns.

3. ```.open FILE``` will open the given file (```.open dog_db.db```) or create one with the given name

4. ```sqlite3 FILE``` will open the given file (```sqlite3 dog_db.db```) or create one with the given name

5. ```.read FILE.sql``` will read (execute) the content inside the given SQL file. 



######Storage Classes and Datatypes

Each value stored in an SQLite database (or manipulated by the database engine) has one of the following storage classes:

1. NULL. The value is a NULL value.

2. INTEGER. The value is a signed integer, stored in 1, 2, 3, 4, 6, or 8 bytes depending on the magnitude of the value.

3. REAL. The value is a floating point value, stored as an 8-byte IEEE floating point number.

4. TEXT. The value is a text string, stored using the database encoding (UTF-8, UTF-16BE or UTF-16LE).

5. BLOB. The value is a blob of data, stored exactly as it was input.

\* There is no Boolean class neither a class set aside for storing dates and/or times

###### Capitalize when using a command

```sql
CREATE TABLE dogs (
    name TEXT,
    breed TEXT,
    age INTEGER
); 
```

```sql
.tables
dogs
```

###### Some command examples with SQL

```sql
CREATE TABLE dogs (
    name TEXT,
    breed TEXT,
    age INTEGER
);

CREATE TABLE cats (
    name TEXT,
    breed TEXT,
    age INTEGER
);

INSERT INTO cats (name, breed, age) VALUES ("Blue", "Turkish", 3);
INSERT INTO cats (name, breed, age) VALUES ("Brownito", "Persa", 5);
INSERT INTO cats (name, breed, age) VALUES ("Whitee", "Argentinian", 2);
INSERT INTO cats (name, breed, age) VALUES ("Kitto", "Siames", 6);
INSERT INTO cats (name, breed, age) VALUES ("Cato", "French", 8);


-- The values must correspond to the columns of the table

SELECT * FROM cats;
-- These means: select EVERY COLUMN from table named cats

-- Could also do:

SELECT * FROM cats WHERE name IS "Cato";

SELECT name FROM cats WHERE breed IS "Persa";

SELECT * FROM cats WHERE breed IS NOT "Persa" AND breed IS NOT "Siames";

SELECT * FROM cats WHERE age > 5;


#The LIKE "%ee%" means: if it contains 2 ee together followed or precedido of anything.
# % stands for: "other stuff"

SELECT * FROM cats WHERE name LIKE "%ee%";
#'Whitee'

```

## Python + SQL

[sqlite3 Python Library - Documentation](https://docs.python.org/3/library/sqlite3.html)


**Connecting to DB, creating a cursor, inserting individual data, commiting and closing**

```py
import sqlite3
conn = sqlite3.connect("my_friends.db")
#Creates a connection; if it already exists, it's just connects straight to it; 
#else, it creates it with the fiven name.

# create cursor object
c = conn.cursor()
#cursor is like a temporary workspace or work area for SQL commands. It allows you to execute lines of SQL with it. 


# execute some sql
c.execute("CREATE TABLE friends (first_name TEXT, last_name TEXT, closeness INTEGER);")
# insert_query = '''INSERT INTO friends 
#                   VALUES ('Merriwether', 'Lewis', 7)'''

data = ("Steve", "Irwin", 9)
query = "INSERT INTO friends VALUES (?,?,?)"
c.execute(query, data)

# commit changes
conn.commit()

#Closes de connection
conn.close()
#Add. Note: this is why finally is in important in the try; except logic: allows you to close connections to, i.e. data bases. 
```

**Inserting bulk of data at once; Inserting bulk of data by looping iterable**

```py
import sqlite3
conn = sqlite3.connect("my_friends.db")
# create cursor object
c = conn.cursor()

people = [
    ("Roald","Amundsen", 5),
    ("Rosa", "Parks", 8),
    ("Henry", "Hudson", 7),
    ("Neil","Armstrong", 7),
    ("Daniel", "Boone", 3)]

# for person in people:
#   insert that one person
average = 0
for person in people:
    c.execute("INSERT INTO friends VALUES (?,?,?)", person)
    average += person[2]
print(average/len(people))

# Insert all at once
# c.executemany("INSERT INTO friends VALUES (?,?,?)", people)

# commit changes
conn.commit()
conn.close()
```

**Selecting (fetching) data from DB**

```py
import sqlite3
conn = sqlite3.connect("my_friends.db")
# create cursor object
c = conn.cursor()
# c.execute("SELECT * FROM friends WHERE first_name IS 'Rosa'")
c.execute("SELECT * FROM friends WHERE closeness > 5 ORDER BY closeness")


# Iterate over cursor
# for result in c:
#   print(result)

# Fetch One Result
# print(c.fetchone())

# Fetch all results as list
print(c.fetchall())


# commit changes
conn.commit()
conn.close()

#fetch significa EXTRAER

```

**SQL injection**

[SQL injection - Colt Steele](https://www.udemy.com/course/the-modern-python3-bootcamp/learn/lecture/10544366#questions/7072584)

SQL injection is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. It generally allows an attacker to view data that they are not normally able to retrieve. This might include data belonging to other users, or any other data that the application itself is able to access. In many cases, an attacker can modify or delete this data, causing persistent changes to the application's content or behavior.

```py
import sqlite3
conn = sqlite3.connect("users.db")

# query = "CREATE TABLE users (username TEXT, password TEXT)"
u = input("please enter your username...")
p = input("please enter your password...")
c = conn.cursor()

# THE BAD WAY!
# query = f"SELECT * FROM users WHERE username='{u}' AND password = '{p}'"

# THE MUCH SAFER WAY
query = f"SELECT * FROM users WHERE username=? AND password =?"
c.execute(query,(u,p))

result = c.fetchone()
if(result):
    print("WELCOME BACK")
else:
    print("FAILED LOGIN")

conn.commit()
conn.close()
```

```py
import sqlite3
import requests
from bs4 import BeautifulSoup

# Request URl

def scrape_books(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    books = soup.find_all("article")
    all_books = []
    for book in books:
        book_data = (get_title(book),get_price(book),get_rating(book))
        all_books.append(book_data)
    save_books(all_books)
    

def save_books(all_books):
    connection = sqlite3.connect("books.db")
    c = connection.cursor()
    c.execute('''CREATE TABLE books 
        (title TEXT,price REAL,rating INTEGER)''')
    c.executemany("INSERT INTO books VALUES (?,?,?)", all_books)
    connection.commit()
    connection.close()

def get_title(book):
    return book.find("h3").find("a")["title"]

def get_price(book):
    price = book.select(".price_color")[0].get_text()
    return float(price.replace("£","").replace("Â",""))

def get_rating(book):
    ratings = {"Zero": 0, "One": 1, "Two": 2, "Three": 3, "Four": 4, "Five": 5}
    paragraph = book.select(".star-rating")[0]
    word = paragraph.get_attribute_list("class")[-1]
    return ratings[word]

scrape_books("http://books.toscrape.com/catalogue/category/books/history_32/index.html")
# Initialize BS
# Extract Data we Want
# Save data to database
```


