# Closures and the decorator pattern

#### Or how to modify the behaviour of functions in Python and JavaScript

> **\[info\] This section is not specific to Reeborg's World**
>
> If you already know how to write your own decorators in Python, you can ignore the content of this appendix.

In this appendix, I will describe how to use the decorator pattern to modify functions in either Python or JavaScript. I will first do it using Python, and then show how to do the same thing using JavaScript.

You already have seen some examples where I have used the decorator pattern

> **TODO**: add references here and give one example, perhaps
>
> ```py
> move = make_slippery(move, "ice")
> ```

When I was learning about decorators, I found that most of the tutorials were too succinct for me to follow easily. Here, I make a point of moving on very slowly in an attempt to make sure that you will be able to get a full understanding of the very useful decorator pattern and be able to write your own when needed.

## Assigning a name to an object in Python

To understand the explanation that follows, I **strongly** urge you to follow along not simply by reading but by reproducing the examples in Reeborg's World.  Using the Python REPL, we can see that `move` is the name of a function:

```py
>>> print(move)
<function move>
```

As you can see \(especially is you try on your own\), using `print` on a function \(without calling it\) tells us that it _**is**_ a function, with a defined "name".  We can use the `=` operator to give another name to this same object

```py
>>> forward = move
>>> print(forward)
<function move>
```

Using the `=` operator to assign our own name does not change anything about the original object, including its name.  You can see this if you use this newly name copy of the original function

```py
>>> forward()  # see the robot moving forward
```

In Python, the "name" of a function is a special attribute which we can access directly:

```py
>>> print(move.__name__)
move
>>> print(forward.__name__)
move
```

## Using `return`

Instead of simply using the `=` operator to assign a new name, as in `forward = move`, we can use a slightly more convoluted way:

```py
>>> def return_move():
...    return move
... 
>>> forward = return_move()
```

Again, we can verify that `forward` defined this way is the same function as the original, either by getting a representation of the function using `print`

```py
>>> print(forward)
<function move>
```

or by actually using it in a program, and calling it: `forward()`.

We can make this even more convoluted by passing as an argument to a function that returns any object passed as an argument:

```py
>>> def return_obj(obj):
...     return obj
... 
>>> forward = return_obj(move)
>>> print(forward)  # checking that it is still the same function
<function move>
```

This may seem like a completely silly example at this point, but it will come in handy before the end of this appendix.

Note that, In all of the examples above, we never call \(directly\) the function `move`[^1], but simply pass its name around so that we can assign new names to the object it represents.

## And now, for something different

Prior to reading this appendix, if I had asked you to define a new function that would make Reeborg **move**, you would likely have done something like this:

```py
def do_move():
   '''my move'''
    move()
```

Indeed, this would work, as calling `do_move()` would do the same as calling `move()` directly.  However, this would be clearly a different function:

```py
>>> def do_move():
...     ''''my move'''
...     move()
... 
>>> print(do_move) # see what object it is
<function do_move>
```

Furthermore, you can check that calling `help(do_move)` gives the following result

![](/assets/my_move_help.png)

whereas calling `help(move)` gives

![](/assets/move_help.png)

So, even though calling `do_move()` has the same effect as calling `move()`, they are completely different object.

However, we can make `do_move()` look identical to `move()` if we redefine its name attribute **and** its docstring as follows:

```py
>>> do_move.__name__ = move.__name__
>>> do_move.__doc__ = move.__doc__
```

This is something you should verify by yourself.

We could do something like this for functions other than `move`; for example:

```py
>>> def do_take():
...     take()
... 
>>> do_take.__name__ = take.__name__
>>> do_take.__doc__ = take.__doc__
>>> print(do_take)
<function take>
>>> help(do_take)  # gives the same result as help(take)
```

We could **repeat** this process for as many other robot instructions as we wanted.  However, we know that repeatedly typing the same series of instructions in a program is a signal that we should define a function that does the repeated pattern for us.

```py
>>> def duplicate(fn):
...     def do_fn():
...         fn()
...     do_fn.__doc__ = fn.__doc__
...     do_fn.__name__ = fn.__name__
...     return do_fn
...

>>> forward = duplicate(move)
>>> print(forward)
<function move>

>>> grab = duplicate(take)
>>> print(grab)
<function take>
```

Usually, instead of the name `do_fn`, people use the name `wrapper` which we shall use from now on.

## Ready to decorate

Instead of duplicating the existing behaviour, let's modify it - or decorate it, as people say. For example, after a successful action \(`move`, `take`, `put`\), let's have Reeborg celebrate by doing a little dance

```py
>>> def celebrate(fn):
...     def wrapper():
...         fn()
...         for i in range(4):
...             turn_left()
...     wrapper.__name__ = fn.__name__
...     wrapper.__doc__ = fn.__doc__
...     return wrapper
... 
>>> move = celebrate(move)
>>> while front_is_clear():
...     move()
...
```

And the result is the following:

![](/assets/celebrate.png)

This is the essence of the decorator pattern: we have a function[^2] \(`celebrate`\) that takes another function as an argument \(`move` in our last example\) and returns ... a modified function[^3] which assign to one that has the same name as the original.

## Closure

The concept of closure is close linked to that of decorator; in fact, the `wrapper` function is a specific example of the use of a **closure**.  If the number of tutorials found on the Internet is any indication, the concept of **closure** seems to be confusing for many people. In what follows, I will expand on the above example to show another example of closure. However, I will first make a small detour and consider something slightly different. Using Python, define the following in the library:

```py
three = 3
def turn_right():
    for i in range(three):
        turn_left()
```

If I ask you to run the following program in the main editor, you will most likely **not** be surprised by the result:

```py
from library import turn_right
turn_right()
```

The variable `three` is not part of the local scope of the function `turn_right`, but it is nonetheless available from within that function. Nothing so far should be surprising or confusing for you \(except for asking yourself why I bother with such a simple example\).

Now, let's go back to our previous `celebrate` example and modify it ever so slightly by introducing a variable named `four`; this time, we write it in a way that makes it easier for you to cut and paste in the editor and run it, instead of using the REPL to evaluate the code one line at a time:

```py
def celebrate(fn):
    four = 4
    def wrapper():
        fn()
        for i in range(four):
            turn_left()
    wrapper.__name__ = fn.__name__
    wrapper.__doc__ = fn.__doc__
    return wrapper

move = celebrate(move)
while front_is_clear():
    move()

# run the above example
# try also print(four) here
```

The variable `four` is not defined outside of `celebrate`; however, it is "known" from within `wrapper` and, since `wrapper` is returned, it is "known" by the redefined `move` which is a new name for the `wrapper` function.  This is the concept of closure: an environment/namespace is available to a function \(`wrapper`\) even though this environment/namespace is no longer in scope for the rest of the program.

In this instance, `celebrate` is somewhat similar to our **library** module in that any function defined within either of them has access to other variables defined within either of them. \[There is of course a difference in that we **can** have access `three` by doing `from library import three`, whereas we cannot have access to `four` from outside the function.\]

Finally, instead of hard-coding the value `four`, we can pass it as an argument to the decorator:

```py
def celebrate(fn, n):
    def wrapper():
        fn()
        for i in range(n):
            turn_left()
    wrapper.__name__ = fn.__name__
    wrapper.__doc__ = fn.__doc__
    return wrapper

move = celebrate(move, 4)
while front_is_clear():
    move()              # new "decorated" move function
```

## Python specific considerations

In Python, the decorator pattern is normally used when **defining** a function, rather than to modify an existing function like we have done so far. Programmers use standard decorators from some libraries to modify functions; for example:

* to log results
* to cache results from a function \(and speed up later calls to the same function\)
* etc.

So, in Python, we might want to write:

```py
def some_function():
    # code here

# immediately modify it using the decorator pattern
some_function = decorator(some_function)
```

This requires us to write the name `some_function` three times.  Python uses a special syntax called a **decorator expression** as a simplified notation to do the above:

```py
@decorator
def some_function():
    # code here
```

This notation avoids having to write the name `some_function` three times, when we are using a pre-defined decorator function.  Note that many people use the name **decorator** both to mean the special syntax \(decorator expression\) **and** to refer to the decorator function itself.

Because we want to preserve some information \(such as the docstring or the name of the function\) when using the decorator pattern in Python, a special decorator named `wraps` is available in the `functools` module of the Python standard library. In general, it is preferable to use code from the Python standard library wherever possible, since it is almost guaranteed to be more efficient and bug-free than code you might write yourself. However, importing this module triggers many other modules import ... and, since Brython requires calls over the internet any time a module is imported, the first time `wraps` is imported causes a noticeable delay in the code execution. I thus recommend that you write your own code instead of using a decorator from the standard library or, **even better**, use some of the decorators I have made available for you as mentioned elsewhere in this book.

# Using Javascript

Except for the special decorator notation using the `@` symbol, all of the important concepts we have shown above also apply for JavaScript. Two minor exceptions are:

1. JavaScript functions do not have a "name" attribute
2. JavaScript functions do not have a docstring.

For Python, we have used `print()` to verify that two functions were identical. JavaScript does not have a `print` function like Python. Instead, if you attempt to call `print()` in a JavaScript program, a print dialog will open, which may look like this if you use Chrome on a French version of Windows ;-\) ![](/assets/print_dialog.png)

You should try it on your own computer to see the result.

This is not very useful for us.  For this reason, I have defined `write()` as a JavaScript function[^4]; `write()` works similarly to Python's `print()` function except that you need to explicitly add new lines characters if you want the next invocation to start on a new line.

So, using JavaScript, if I execute

```js
write(move);
```

the result will be ... **undefined**.  This is not very useful.  Perhaps some thing more useful is to ask JavaScript to give us a string representation of the object `move`

```js
write(move.toString());
```

As I write this book[^5], the result is as follows

```js
function () {
    RUR.control.move(RUR.get_current_world().robots[0]);
}
```

You can try the following and see that you will get the same result whether you use `move` or `forward`.

```js
forward = move;
write(move.toString());
write(forward.toString());
```

This should confirm to you that the name `forward` refers exactly the same underlying object.

So, for JavaScript, like for Python, using the `=` operator simply assigns a new name to the same underlying object.

We can also reassign using the `=` operator and `return`  as we had done with Python; you can easily verify by running the following program:

```js
function return_obj(obj) {
    return obj;
}
forward = return_obj(move);
write(forward.toString());  // same as before

// Of course, we could call it
forward()
```

Finally, we can reproduce our `celebrate` example in JavaScript.  Since JavaScript functions do not have docstrings nor a "name" attribute, the code is slightly simpler:

```js
function celebrate(fn) {
    function wrapper() {
        fn();
        for (var i=0; i < 4; i++) {
            turn_left();
        }
    }
    return wrapper;
}

move = celebrate(move);

while (front_is_clear()) {
    move();
}
```

[^1]: I never wrote `move()` in any of the examples above; only `move`, without the parentheses, \(\).

[^2]: Instead of a function, we could have some other callable, such as a Python class.

[^3]: Some people say that something else than a function could be returned and that it should still be called a decorator.

[^4]: In French, use `ecrit()`.

[^5]: You may see a different result if I change the program in the mean time.

