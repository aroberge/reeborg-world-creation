# Closures and the decorator pattern

#### Or how to modify the behaviour of functions in Python and JavaScript

If you already know how to write your own decorators in Python, you can ignore the content of this appendix.

In this appendix, I will describe how to use the decorator pattern to modify functions in either Python or JavaScript. Most of the examples will be given using Python, but, whenever it makes sense, I will make a point of showing how to reproduce using JavaScript the main ideas demonstrated with Python.

If you are not familiar with the decorator pattern, I strongly urge you to follow along not simply by reading the explanations but by reproducing and ideally modifying them in Reeborg's World.

When I was learning about decorators, I found that most of the tutorials were too succinct for me to follow easily. Here, I make a point of moving on very slowly in an attempt to make sure that you will be able to get a full understanding of the very useful decorator pattern and be able to write your own when needed.

## Assigning a name to an object

Using the Python REPL, we can see that `move` is the name of a function:

```py
>>> print(move)
<function move>
```

We can use the `=` operator to give another name to this same object

```py
>>> forward = move
>>> print(forward)
<function move>
>>> forward()   # see the robot moving forward
```

As you can see \(especially is you try on your own\), using `print` on a function \(without calling it\) tells us that it _**is**_ a function, with a defined "name".  Using the `=` operator to assign our own name does not change anything about the original object, including its name.  In fact, we can get at the "name" of the function as follows:

```py
>>> print(move.__name__)
move
>>> print(forward.__name__)
move
```

JavaScript does not have a `print` function like Python. Instead, if you attempt to call `print()` in a JavaScript program, a print dialog will open, which may look like this if you use Chrome on a French version of Windows ;-\) ![](/assets/print_dialog.png)

You should try it on your own computer to see the result.

This is not very useful for us.  For this reason, I have defined `write()` as a JavaScript function[^1]; `write()` works similarly to Python's `print()` function except that you need to explicitly add new lines characters if you want the next invocation to start on a new line.

So, using JavaScript, if I execute

```js
write(move);
```

the result will be ... **undefined**.  This is not very useful.  Perhaps some thing more useful is to ask JavaScript to give us a string representation of the object `move`

```js
write(move.toString());
```

As I write this book[^2], the result is as follows

```js
function () {
    RUR.control.move(RUR.get_current_world().robots[0]);
}
```

You can try the following and see that you will get the same result whether you use `move` or `forward`.

```js
forward = move;
write(forward.toString());
```

This should confirm to you that the name `forward` refers exactly the same underlying object.

## Assigning a name to an object using `return`

We can use a slightly more convoluted way to assign a new name to `move`.

```py
>>> def return_move():
...    return move
... 
>>> forward = return_move()
>>> print(forward)
<function move>
```

We can make this even more convoluted by passing as an argument to a function that returns any object passed as an argument:

```py
>>> def return_obj(obj):
...     return obj
... 
>>> forward = return_obj(move)
>>> print(forward)
<function move>
```

We can also do the same thing in JavaScript, as you easily verify by running the following program:

```js
function return_obj(obj) {
    return obj;
}
forward = return_obj(move);
write(forward.toString())

// Of course, we could call it
forward()
```

We could also do a circular assignment, by re-assigning the name `move` to refer to the original function of the same name:

```py
>>> def return_obj(obj):
...     return obj
... 
>>> move = return_obj(move)
>>> print(move)
<function move>
```

This may seem like a completely silly example at this point, but it will come in handy before the end of this appendix.

Note that, In all of the examples above, we never call \(directly\) the function `move`[^3], but simply pass its name around so that we can assign new names to the object it represents.

[^1]: In French, use `ecrit()`.

[^2]: You may see a different result if I change the program in the mean time.

[^3]: We never wrote `move()` in any of the examples above.

