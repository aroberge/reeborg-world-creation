# Exploring and getting help

In the previous section, I mentioned the [Application Programming Interface \(API\)](http://reeborg.ca/api/RUR.html) which you should definitely consult in parallel with this book when creating your own worlds.  However, there are other ways available for you to get help.

Even if you use only one of either Python or JavaScript in your teachingt, both have complementary tools which might be useful to know.

> **\[info\] Images may look different from what you see** 
>
> In the examples below, I have ajusted the size of the windows prior to taking screenshots.

## Using Python

From either the editor or the Python REPL, you can also get some _help_:

* To list all available Python functions, classes, etc., simply enter `help()`.
* To get help about a particular function, for example `move`, enter `help(move)`
* To get a complete, up-to-date version of every Python function available in the English version, enter

  ```python
    import reeborg_en
    help(reeborg_en)
  ```

  You can use `reeborg_fr` to get the corresponding French version. \[**Suggestion**: if you teach using a language other than English or French, I will gladly add a version in your own language ;-\)\] Note that this help system is specific to Python and does **not** include the available functions prefixed by `RUR` and documented in the the [Application Programming Interface \(API\)](http://reeborg.ca/api/RUR.html). With a few exceptions, if a function exists in Python \(e.g. `move()`\), there is one with the same name also available when using Javascript.

If you are familiar with Python, you likely already know about `dir()`. This Python built-in function is great in finding out the various attribute of an object. For example, executing

```py
r = UsedRobot()
print(dir(r))
```

lists the attributes \(methods and variables\) belonging to this object.  If you do this, you might notice the `body` attribute, perhaps inviting you to see what attributes it has, if any.

```py
r = UsedRobot()
print(dir(r.body))
```

If you run these two examples from the REPL, the output will be printed in a reasonably acceptable format. However, if you do it from the Python code editor, the output may require you to do a lot of scrolling to find out what information is available.

![](/assets/print_dir.png)

For your convenience, I have included a new function, `print_dir()` which prints the result in a more user friendly way.

**However**, please note that, for the first of these two specific examples, it would have been much better to do the following:

```py
r = UsedRobot()
help(r)
```

## Using JavaScript

In a previous version of Reeborg's World, I had included a function, `dir_js` which could be used somewhat like Python's `dir()`. There was also a function named `inspect()` and another named `view_js_source()` which were useful for exploring the code in different ways. In this new version of Reeborg's World, I have simplified the approach, eliminating the old functions and introducing a new one currently named `help_js()`. 

> **\[success\] Feedback wanted**
>
> Can you think of a better name to use instead of `help_js` ?

Here are the equivalent to the two Python examples I mentioned above:

```js
r = new UsedRobot();
help_js(r)
```

![](/assets/help_js_r.png)

```js
r = new UsedRobot();
help_js(r.body);
```

![](/assets/help_js_body.png)

As you can see, the output is both better looking and more informative than the corresponding one from Python.

If I instead use it for a function/method,

```js
r = new UsedRobot();
help_js(r.move);
```

I get the actual code of that function:

![](/assets/help_js_r_move.png)

which I can then explore further,

```js
help_js(RUR._UR.move_);
// after looking at the output, I then try
help_js(RUR.control.move);
```

![](/assets/help_js_move.png)

> **\[success\] Tip**
>
> Instead of going to Github and browse the code repository to find out the implementation details, it might be more effective to use `help_js()` as shown above.

## About RUR

Previously, I mentioned that there are a lot more functions belonging to the RUR namespace than what I have documented in the [Application Programming Interface \(API\)](http://reeborg.ca/api/RUR.html). You can actually see all the names belonging to that namespace by doing `help_js(RUR)`. However, only those documented in the API are \(reasonably\) guaranteed not to change.





