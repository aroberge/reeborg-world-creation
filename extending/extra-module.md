# Extra module

Suppose that you would like to provide your students with additional functions or classes predefined. For example, you might want your student to use `turn_right()` without having to create such a definition themselves, or have a `RepairedRobot` which fixes many of the limitations of the default `UsedRobot`. You can do so by creating content for a special library module called **extra**. Once "installed" \(in the browser's memory\), students can use this content as though this was a standard Python module.

```py
from extra import turn_right, RepairedRobot
```

Alternatively, **you **can do this code importation in the Pre editor which is executed just before the student's program: you can thus provide students with additional functions without requiring them to have to know how to use an explicit import statement.

### Creating the extra module

Creating this module is done via a single function call:

```py
RUR.set_extra_content(python_code)
```

where `python_code` is a string. For example, you could have

```py
RUR.set_extra_content('''
def turn_right():
    turn_left()
    turn_left()
    turn_left()
'''
```

However, in my opinion, this is not the simplest way. Instead, when creating a world for your students, you can put the content which you plan to have in the extra module either in the Python code editor or in the library.  Then, when you save the world, you have to select the option to include the code contained in the relevant editor tab so that the code will be included.  In the Onload editor you can then include the following:

```py
RUR.onload_set_programming_language("python")

# Either:
RUR.set_extra_content(RUR.get_editor_from_world())
# or
RUR.set_extra_content(RUR.get_library_from_world())
```

An example is provided in

```py
# example world to be included here.
```

By default, the code will be shown in an additional editor tab in read-only mode.  If you do not wish to have this tab shown, include a second parameter \(`hidden`\) set to `True` when setting the content:

```py
RUR.set_extra_content(python_code, True)
```

Note that this is a JavaScript function \(but, like all the others belonging to the `RUR` name space, it can be called from a Python program\) and that the second argument is a positional argument and not a keyword argument, even though I referred to this parameter by the name `hide`.

### What about JavaScript?

JavaScript, at least as it currently exists, does not have a statement similar to Python's `import`.  However, by defining a global object \(as attribute to `window`\) you can make additional functions available for other programs executed with JavaScript.  For example, you may want to try adding the following:

```js
window.turn_right = function () {
    turn_left();
    turn_left();
    turn_left();
};
```

.After executing this program, you should be able to use `turn_right()` in any subsequent programs written in JavaScript.  You could include such definitions in the Onload part of a special world that student would load first, and then be able to use such definitions at any time in a given session.

