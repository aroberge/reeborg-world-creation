# Built-in randomness

Having well-defined worlds is nice, but it is sometimes useful to be able to see if students can write programs general enough to address a whole range of situations. To this end, Reeborg's World easily supports designing worlds with some randomly chosen values but in a way that is very visible to the students when they load the world.  This is different than the last example from a previous chapter,

```py
World("worlds/examples/river_demo.json", "Crossing the river")
```

where we were using Python's random module to select a secret location \(not visible to the student\) where Reeborg could cross a river.

> **\[warning\]**
>
> The examples given in this chapter should only be used for _creating_ worlds, either by writing the code only in the Onload editor or by saving the world in a json file and removing the code.

## Random number of objects

To specify a random number of objects at one location, one needs to use the attributes `min` and `max` as follows:

```py
RUR.add_object("token", 2, 1, {"min":2, "max": 5})
```

Instead of a number, we see a "**?**" next to the token, indicating an unknown quantity. However, a user can see the range of possible values by using the **World Info** dialog.

![](/assets/token_random.png)

When a user clicks on the _run_ or _step_ button, before their program is actually executed, a special function is called \(`RUR.world_init`\) to identify values that should be chosen at random within a certain range, and set them, after which the code entered by the user is run. If other random values are introduced afterwards, they may yield inconsistent states.

This is why you should use code like the above in one of two ways only as mentioned previously:

1. write the above code in the **main editor**, run the program and save the result in a .json file;
2. write the above code in the **Onload** editor, and save the world including that code.

## Setting goals with random values

Before we had considered the possibility of starting with random values, we had seen how to specify a goal requiring a specific number of objects to be put at one location. But how can we deal with situations where the total number of objects is set randomly? One simple way is to require all the objects to be put at a single location and use the value `"all"` as a goal, as follows:

```py
RUR.add_object("token", 2, 1, {"min":2, "max": 5})
RUR.add_object("token", 3, 1, {"min":0, "max": 4})
RUR.add_object("token", 4, 1, {"goal":"all"})
```

## Random initial and final positions

In the very first example, in the second instruction, we showed how to set up a final position as a goal:

```py
RUR.set_world_size(3, 3)
RUR.add_final_position("house", 3, 1)
RUR.add_wall("east", 1, 1)
```

Repeated calls to this method, with different coordinates, result in a final position that will be chosen at random.  
The same can be done for the starting position. For example, assuming we start with a robot at position `(1, 1)`  
we can set up additional possible initial positions chosen randomly, and possible final positions also chosen randomly,  
by something like the following \[and illustrated below\].

```py
RUR.add_initial_position(1, 2)

RUR.add_final_position("house", 3, 1)
RUR.add_final_position("house", 3, 2)
RUR.add_final_position("house", 3, 3)
```

| We start with a world with a single robot. | ![](/assets/random1.png) |
| :--- | :--- |
| We added a second \(possible\) initial position; the images are dimmed, providing a visual clue that choices are possible. | ![](/assets/random2.png) |
| Adding a first final position. | ![](/assets/random3.png) |
| Adding a second final position; these images are dimmed. | ![](/assets/random4.png) |
| After adding the third final position. | ![](/assets/random5.png) |

To indicate that a choice will be made, the images \(for the robot, or the final destination\) are made partly transparent when there is more than one possible choice. Later, when the program is executed with this world as a starting point, the very first step is to randomly make a selection among the possible values.

## Random orientation

Random orientations are shown ... by the robot changing orientation randomly \(!\) and constantly; it cannot be adequately shown by static screenshots.

Select world **Alone**, or any other world with a robot already in it.  Then enter the following program and run it:

```py
RUR.set_random_orientation()
pause(3000)
RUR.add_initial_position(3, 3)
```

Perhaps your students are ready to write a program to reliably solve the following task:

```py
World("worlds/examples/very_random.json", "Very random")
```

This last example could have been created using the menu-driven World editor; however, I used methods in the **Onload **editor as you can see if you click on **World Info**.

