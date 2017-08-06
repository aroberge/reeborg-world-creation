# Python code pre-processing: the gory details

As far as I know, most if not all Karel simulators implement their own code interpreter, so that students can step through instructions one at a time.  However, this is not the case for Reeborg's World.  The reason for this is that I wanted for anyone using the program to be able to use **any** valid Python or Javascript code, and I am not competent enough to implement a fully-featured JavaScript or Python interpreter.  Here is what I do instead.

## Javascript

I concatenate the code found in the Pre editor \(written by the creator of the world\) with the user's code and the code found in the Post editor \(also written by the creator of the world\). Then, I use Javascript's `eval()` to execute the program. This can essentially be summed up by:

```js
eval(Pre + program + Post)
```

During the execution, each time the world changes \(e.g. Reeborg changes position using `move()`\), a copy of the world's content is made \(which I call a frame\) and appended to an Javascript array \(similar to a Python list\). When `eval()` terminates, the content of that array is displayed frame by frame with a user-definable interval \(using `think()`\) between each frame; this is done using Javascript's `setTimeout` function.

The initial reason why I used a recording of frames was that Javascript is a single-threaded language which does have a `sleep()` function - otherwise, I would have likely used this. However, since I use a list of frames, students can not only step forward through the recording but also backwards if they so desire, which would not have been possible with using an approach based on the existence of a `sleep()` function.  With the approach used, students can even quickly go through a particular frame using the html slider.

#### Dealing with Javascript errors

Reeborg's World uses Javascript Errors / Python Exceptions to signal the end of a user's program - sometimes after some analysis to confirm that the task was accomplished successfully \(or not\). So, the code run is closer to this:

```js
try {
    eval(Pre + program + Post);
} catch (e) {
    analyze_error(e);
}
// If there was not a fatal error:
display_result_frame_by_frame()
// after last frame, 
if (wold_includes_goal()) {
   check_goal();
}
```

The error analysis and goal checking consists essentially in formatting the information received and presenting it to the user.

![](/assets/good_result.png)

![](/assets/bad_result.png)

## Python - no highlighting

By default when using Python, highlighting of a line of code about to be executed is performed. This can be turned off. In this case, processing of code written in Python closely matches how it is done with Javascript.  The Python interpreter used is [Brython](http://brython.info/). Instead of using `eval()`, `exec()` is used with something like the following:[^1]

```py
import reeborg_en
globals_ = {}
exec(reeborg_en, globals_)  # see note 1 below
program = transform(program)
exec(Pre + program + Post, globals_)
```

Once again, frames are recorded and playback is done using Javascript's `setTimeout`.

The function `transform()` scans the user's code as a string \(i.e. it does not evaluate its validity\) and replace any instance of

```py
repeat n:
    block_of_code
```

by

```py
for count_variable in range(n):
    block_of_code
```

where each required `count_variable` is chosen to be a unique name in _program_, and with the additional requirement that `int(n)` must not raise an exception.  Thus `int( 2 * 3)` would be valid, but `int(variable)` where `variable` is a valid Python identifier would not be valid.

#### Additional processing: non-breaking space

In addition to the above, non-breaking spaces \(html `&nbsp;`  or `&\#160;`\) are transformed into regular spaces \(ASCII 32\). This is to allow users to copy code from a teacher's website or from the [API page](http://reeborg.ca/api/RUR.html) into the editor and have it executed correctly. Python does not recognize this character as a valid space character, whereas Javascript does.

#### The library

The true library module is not the one seen by the student. Here is its true content:[^2]

```py
from browser import window
from preprocess import transform
from reeborg_en import *
src = transform(window.library.getValue())
exec(src)
```

The function `window.library.getValue()` gets a copy of the code in the library editor tab and transforms it so that `repeat` can also be used.

#### Dealing with Python Exceptions

Like for Javascript, we also do some analysis at the end of a program.  The analysis performed is however more extensive. If we find a `SyntaxError`, we examine the code and attempt so see if perhaps a colon `:` is missing to indicate the beginning of a block of code, or if parentheses `()` might be missing in a function call. We also try to identify the line of code in the user's program where the error occurred; however, this is not always reliable since the code executed potentially include some additional code in the Pre editor and also some extra lines of code inserted to provide code highlighting and watching variables as described below. We do a similar search for the line number when an `IndentationError` is raised and try to the same for a `NameError`.

## Python - with highlighting

When code highlighting is desired, some extra processing on the user's code is done to insert additional statements, each indicating which line or lines of code must be highlighted. For example, with code highlighting on, a user may enter the following program in the editor:

```py
def turn_right():
    repeat 3:
        turn_left()

def follow_wall():
    '''
        Useful for getting out of a maze
    '''
    if right_is_clear():
        turn_right()
        move()
    elif front_is_clear():
        move()
    else:
        turn_left()

while not at_goal():
    follow_wall()
```

and the program actually executed will be the following:

```py
RUR.set_lineno_highlight([0])
def turn_right():
    RUR.set_lineno_highlight([1])
    for ITERATION_VARIABLE0 in range(3):
        RUR.set_lineno_highlight([1])
        RUR.set_lineno_highlight([2])
        turn_left()

RUR.set_lineno_highlight([4])
def follow_wall():
    RUR.set_lineno_highlight([5, 6, 7])
    '''
        Useful for getting out of a maze
    '''
    RUR.set_lineno_highlight([8])
    if right_is_clear():
        RUR.set_lineno_highlight([9])
        turn_right()
        RUR.set_lineno_highlight([10])
        move()
    elif RUR.set_lineno_highlight([11]) and front_is_clear():
        RUR.set_lineno_highlight([12])
        move()
    else:
        RUR.set_lineno_highlight([13])
        RUR.set_lineno_highlight([14])
        turn_left()

RUR.set_lineno_highlight([16])
while not at_goal():
    RUR.set_lineno_highlight([16])
    RUR.set_lineno_highlight([17])
    follow_wall()
```

Frome the various tests I have done, this code insertion seems to be reliable when the user's program contains neither  `SyntaxError` nor `IndentationError`. However, I consider it to be potentially fragile. If you see an `Exception` being raised that you cannot explained, you might want to try to turn off highlighting and see if it solves the problem.  If it does, please send me a copy of the offending code so that I can improve the extra processing.

## Watching variables

When watching variables is enabled, yet more extra code gets added.  With both highlighting and watching variable enabled, the simple program

```py
def add_and_print(a, b):
    c = a + b
    print(c)
    return c

add_and_print(3, 5)
```

gets converted to

```py
def add_and_print(a, b):
    __watch(system_default_vars, loc=locals(), gl=globals())
    RUR.set_lineno_highlight([1])
    c = a + b
    __watch(system_default_vars, loc=locals(), gl=globals())
    RUR.set_lineno_highlight([2])
    print(c)
    __watch(system_default_vars, loc=locals(), gl=globals())
    RUR.set_lineno_highlight([3])
    return c

__watch(system_default_vars, loc=locals(), gl=globals())
RUR.set_lineno_highlight([5])
add_and_print(3, 5)
__watch(system_default_vars, loc=locals(), gl=globals())
```

Prior to execution of this code, a copy of variables found in `locals()` is made and copied in `system_default_vars`; these are assumed never to appear in a user's program. Each call to `__watch` potentially result in an extra frame being created; actually, the content of what would be generated by `__watch` in a new frame is actually copied into the previous frame's content to minimize the amount of frames created.

[^1]: Rather than calling `exec()` each time, for efficiency I now call it once at the beginning of a browser session, save the result in a `dict` and update the `locals()` using the saved result. However, I believe that the above code faithfully describes the basic idea of what is actually done.

[^2]: A similar improvement to that noted in [^1] has been made to the code since it was written.

