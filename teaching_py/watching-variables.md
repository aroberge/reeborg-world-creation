# Watching variables

> [Python Tutor](http://www.pythontutor.com/visualize.html), created by[Philip Guo](http://www.pgbovine.net/), helps people overcome a fundamental barrier to learning programming: understanding what happens as the computer runs each line of source code.
>
> Using this tool, you can write [Python](http://www.pythontutor.com/visualize.html#py=2), [Java](http://www.pythontutor.com/java.html), [JavaScript](http://www.pythontutor.com/javascript.html), [TypeScript](http://www.pythontutor.com/typescript.html), [Ruby](http://www.pythontutor.com/ruby.html), [C](http://www.pythontutor.com/c.html), and [C++](http://www.pythontutor.com/cpp.html) code in your web browser and visualize what the computer is doing step-by-step as it runs your code.

Python Tutor is a **proper** code visualizer; it is an excellent tool to use in demonstrating what happens step by step as one runs a program. It is done using appropriate tools such as a debugger.

By constrast, Reeborg's World "watch variables" features is a hack, one that is most likely fragile.  In the appendix **JavaScript and Python code pre-processing: the gory details**, I give a very brief explanation of how it is implemented.

As a quick comparison, if you go to the [Python Tutor main page](http://www.pythontutor.com/), you will see a visualization of the following code:

```py
def listSum(numbers):
  if not numbers:
    return 0
  else:
    (f, rest) = numbers
    return f + listSum(rest)

myList = (1, (2, (3, None)))
total = listSum(myList)
```

And here's how the visualization done by "Reeborg watching variables" looks like:

![](/assets/python_tutor.gif)

With both Python Tutor and Reeborg's World you can look at individual "frames". What is recorded in each frame is different for each visualizers.  By default, Reeborg's World focuses on showing the contents of the `locals()` and `globals()` dict, highlighting in **red** any variable whose value changed from a previous frame. Also, I should note that I have not been able to implement a reliable way to record values corresponding to the last line of a given code block; this likely explains why the above example has fewer recorded frames than shown on the Python Tutor \(even with the addition of two frames for `think()` and `pause()`\).

One feature that is unique to Reeborg's World "watch variables" implementation is the ability to add any expression to a watch list.

![](/assets/watch_vars2.gif)In the above example, we added two expressions to watch:

```py
add_watch("carries_object()")
add_watch("position_in_front()")`
```

We could have added any valid Python expressions, such as `"some_list[3:6]"`, `"a + b * 2"`, etc.  This unique feature might make it worthwhile to consider using it instead of some other visualizers like the Python Tutor.



