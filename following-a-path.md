# Following a path

In this section, I consider a very simple example which requires the student to have Reeborg following a predefined path to reach its home. The end goal is to come up with code \(in the Pre and Post editors\) which can verify that the correct solution has been found. I am using this simple example to explore some of the issues one needs to consider when designing a custom goal based on the perceived capabilities of the students.

![](/assets/easy_path.png)

No obstacle exists in this world, so, a-priori, Reeborg could take any path and achieve the goal. However, we want Reeborg to not walk on the grass and take the minimum amount of instructions possible; here's a simple solution in Python:

```py
World("worlds/examples/easy_path.json") # I will no longer include this line below
move()
move()
turn_left()
move()
```

And here's a completely equivalent solution:

```py
while front_is_clear():
    move()
turn_left()
move()
```

This type of problem could be equally suitable for beginners, with a simple world like this one, or for very advanced students who have to find the shortest path to accomplish a given task in a maze-like world generated randomly each time it is run.

## Finding the path

The first step is to find the correct path; by path, I mean which grid locations must visited other than the starting point.  In this particular case, it is trivial:

```
desired_path = [(1, 2), (1, 1), (2, 1)]
```

However, for more complicated paths, it might be tedious to type in the path; assuming we can write a solution to the problem, it is much easier to let Python do the work for us.

```py
desired_path = []
def m():
    move()
    desired_path.append(position_here())

while front_is_clear():
    m()
turn_left()
m()
print("desired_path =", desired_path)
```

It is then a simple matter of using copy-paste to get the desired result.  Alternatively, we could write this code in the Onload editor and make it accessible later by defining

```py
window['desired_path'] = desired_path
```

## First solution

Here is a first solution where I will assume that we don't want to write the desired path in the Onload editor, using the other editors instead.

```py
# This code would be in the Pre editor

# I use names starting with underscore, asking
# the students not to do this for their own names

_desired_path = [(1, 2), (1, 1), (2, 1)]
_old_move = move
_actual_path = []

def move():
    '''Redefining move'''
    _old_move()
    _actual_path.append(position_here())


#-----------------
# This could be the code written by the student

move()
move()
turn_left()
move()

#-----------------------
# This code would be in the Post editor

if _actual_path != _desired_path:
    raise ReeborgError("The correct path was not followed")
```

This solution would be work with most beginners.  However, there is an easy way to cheat.  Here's such a cheating program:

```py
turn_left()
move()
for i in range(3):
    turn_left()
move()
move()
done()  # !!
```

What we need to do is to prevent the student from using `done()` to bypass the custom evaluation of the goal at the end. This can be done by adding the following to the code in the Pre editor.

```py
def done():
    raise ReeborgError("You cannot use done() in your program!")
```

If we do this, and we try the following:

```py
turn_left()
move()
for i in range(3):
    turn_left()
move()
move()
```

the error message telling us that the correct path has not been followed will appear only at the very end. This may be acceptable in some situations but it is generally better to show immediately when an error occur.

## A second solution

Here is a second solution which informs the student as soon as the correct path is no longer followed.

```py
# This code would be in the Pre editor

# I use names starting with underscore, asking
# the students not to do this for their own names

_desired_path = [(1, 2), (1, 1), (2, 1)]
_old_move = move

def move():
    '''Redefining move'''
    global _desired_path
    _old_move()
    try:
        x, y = _desired_path[0]
    except IndexError:
        raise ReeborgError("The correct path was not followed")

    if position_here() != (x, y):
        raise ReeborgError("The correct path was not followed")

    # remove first element
    _desired_path = _desired_path[1:]

def done():
    raise ReeborgError("You cannot use done() in your program!")

#-----------------
# This could be the failing code written by the student

turn_left()
move()
for i in range(3):
    turn_left()
move()
move()


#-----------------------
# We don't need to add anything in the Post editor
```

This second solution achieves the goal of informing the student as soon as the correct path is no longer followed. However, it is possible to write a program that cheats:

```py
turn_left()
_old_move()
for i in range(3):
    turn_left()
_old_move()
_old_move()
```

Or, without cheating, one can write a program that makes too many left turns:

```py
move()
move()
for i in range(5):
    turn_left()
move()
```

To take care of the second problem, we can redefine `left_turn()` like we did for `move()`by adding the following:

```py
_desired_turns = [(1,1)]
_old_turn_left = turn_left

def turn_left():
    '''redefining turn_left'''
    global _desired_turns
    _old_turn_left()
    try:
        x, y = _desired_turns[0]
    except IndexError:
        raise ReeborgError("The correct path was not followed")
    if position_here() != (x, y):
        raise ReeborgError("The correct path was not followed")
    # remove first element
    _desired_turns = _desired_turns[1:]
```

## A better solution

With the above version, students can still "cheat" by using `_old_move` or `_old_turn_left`.in their program.  Also, if they do `help(move)`, they will get the wrong information \[this could easily be corrected, but it is one more detail to take care of\].

Given that the students have access to all the code running in their browser, programming tasks in Reeborg's World should normally only be assigned as learning exercises and not in exam situations. Nonetheless, it is possible to write code that prevents such cheating from taking place, and avoid having to repeat some tedious code. This is done by using the **decorator pattern**.  If you are not familiar with it, I encourage you to read the appendix **Closures and the decorator pattern**.

