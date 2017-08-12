# Using the Python REPL

If you have learned Python from a traditional tutorial, or have used it somewhat extensively, you are no doubt familiar with its REPL.   REPL is an acronym meaning Read-Eval-Print Loop.  Python's REPL mode presents you a prompt, most often written as `>>>` and waits for some input from you.  When you type in some code and press enter:

* Python **reads** your input and parses it;
* it **evaluates** the statement in the current context;
* it **prints** some result automatically without requiring you to type in an explicit `print()` call
* it **loops** back to its original state where it waits for your input.

The REPL in Reeborg's World is based on the one written by Pierre Quentel for Brython, itself adapted from a similar interpreter in Python's standard library.

Using the REPL mode is different from entering code in the editor and running it.

* Each line of code is processes automatically, as soon as it is entered.  If more code is expected \(for example, a bracket has not been closed or a code block has not been terminated\), a secondary prompt, `...` is shown indicating that more input is expected.
* When loading a world, both the code in the **Onload** editor _**and**_ the code in the **Pre** editor are executed automatically.
* For the robot in the world, no frame is evaluated: the state of the world is immediately updated.  Thus, if we start with ![](/assets/repl_world1.png)

  and enter the following code

```py
>>> while front_is_clear():
...     move()
...
```

the following will be shown immediately, without any animation indicating that a movement is taking place.![](/assets/repl_world2.png)

* In REPL mode, the function `done()` has been changed so that it runs the code in the **Post** editor and automatically evaluate to see if an goal defined in the world has been accomplished. Unlike the "normal" mode, one can have other code processed after calling `done()`; in fact, one can call `done()` multiple times without having to reload the world.
  * If `done()` has been redefined in a given world to prevent a student from using it \(as described in some examples discussed elsewhere\), one can use `Done()` instead; this only works in the REPL mode.
* Commands entered in the REPL are saved in a "history" buffer; navigation in that buffer is done using the UP and DOWN arrow keys.
* In addition to importing code from the library and the extra module \(described elsewhere\), one can import the code currently in the editor using the standard notation, as in `import editor` or `from editor import something`.
* Using the REPL does not change the code in the Python editor. Thus one can easily switch back and forth between the two modes without worrying about making changes in one mode that could affect the other.

The Python REPL mode can be used to quickly find out some useful information:

```py
>>> import reeborg_en
>>> help(reeborg_en)
>>> RUR.show_all_things()
>>> RUR.show_all_robots()
>>> RUR.show_all_things('fatal')
```

## What about JavaScript?

There is no corresponding REPL in JavaScript specially designed  ... **except** that you can always enter some JavaScript command in the browser's console.  This will work most of the time; however, if an error is raised \(for example, you ask Reeborg to `move()` straight into a wall\), you will not see the usual information appearing on the screen.

Since almost all JavaScript functions, such as `move()`, `turn_left()`, etc., are the same as the Python ones, you can use the example given above for Python to find out which commands are available, or which "things" or robots are available.

