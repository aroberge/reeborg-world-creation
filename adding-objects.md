# Adding objects

**Objects**, together with **walls** are the basic elements used to create interesting programming tasks. In this section, we show how to add objects using the [Application Programming Interface \(API\)](http://reeborg.ca/api/RUR.html) instead of using the menu-driven World editor. While it might be easier to use the World editor for objects included with Reeborg's World, using the API is required when it comes to adding your own custom objects.

## Adding a single object

You can add a single object as follows:

```py
 RUR.add_object("token", 3, 4)
```

The result will look similar to the following image:

![](/assets/token_added.png)

Note the number 1 in black, at the bottom left: this is the number of token at that location.  We can add more tokens at that location by repeated calls to this method. A better way is to use an optional argument to specify the additional number of tokens we wish to add.

```py
RUR.add_object("token", 3, 4, {"number":7})
```

![](/assets/token_added7.png)

In the code above, I have written `"number"` as a string so that it could be used with either Python or Javascript; in Javascript, I could have simply written `{number: 7}` and it would have been valid.

## Setting a goal

As a programming task, suppose we wish Reeborg to move these tokens to another location: we can specify this with the `goal` attribute.

```py
  RUR.add_object("token", 3, 4, {"number":7})
  RUR.add_object("token", 4, 4, {"number":7, "goal":"true"})
```

![](/assets/token_goal7.png)

Here again, in order to have a program that can work with either Python or Javascript, I have used a string, `"true"`, as the value of the `goal` attribute. If I knew beforehand that I was only going to use this code in a Python program, for greater clarity, I would have used `True` as follows:

```py
RUR.add_object("token", 3, 4, {"number":7})
RUR.add_object("token", 4, 4, {"number":7, "goal":True})
```

Save for one exception, which we will explain in the next chapter, anything that is evaluated as `"true"` \(i.e., which does not evaluate as `"false"`\) can be used as a value for `"goal"`, leading to the same result.  My **recommendation**: be explicit and use `True/False` in Python and `true/false` in Javascript.

A few things to note:

* As a convention, I have chosen to include grey-level version of the images used for the object to indicate a goal; while I would not recommend it, you could choose a different convention when adding your own objects. For example, you could use the image of a basket in which to collect objects of a given kind.
* The number of objects to put as a goal is indicated at the bottom **right**.
* The number of actual objects, at the bottom **left** is no longer written in black in the example above, but in red: this gives a visual clue.  By comparison, if we specify positions of objects such that the goal is already met:

```py
RUR.add_object("token", 3, 4, {"number":7})
RUR.add_object("token", 3, 4, {"number":7, "goal":"true"})
```

![](/assets/token_goal_met.png)

The number of objects is now indicated in green, giving a visual clue that the goal has been met. Admittedly, using red/green as visual clues will not be useful for all users. This can be changed using

```py
RUR.configure_red_green("red replacement", "green replacement")
```

where the colour choice can be either HTML named colours, decimal colours \(like `"#123456"`\), RGB values, etc.  This colour preference is saved in the browser so it does not have to be redone each time Reeborg's World is loaded by the user on their computer.

## Aside: requiring to build a wall as a goal

Using a syntax similar to that of requiring that an object be placed at a certain location, one can require that a certain wall be built.

```py
RUR.add_wall("north", 3, 3)
RUR.add_wall("east", 3, 3, {"goal":True})
```

A wall that needs to be built is indicated by a dashed line, instead of a solid rectangle for an existing wall.

![](/assets/wall_goal.png)

## Adding multiple objects

If two different kinds of objects are put at the same location, the number is replaced by a question mark.

```py
RUR.add_object("token", 3, 4, {"number":7})
RUR.add_object("tulip", 3, 4, {"number":5})
```

![](/assets/token_tulip.png)

However, by cliking on **World Info**, and then clicking at a given location, the information about how many objects are found at that location is still available to the user.

![](/assets/objects_at_position.png)

## You can add anything as an object

While the menu-driven dialog restricts what you can add as objects, using the API you can add anything ... even it it might not make sense to do do. For example, with the world **Alone **selected, try running the following program

```py
RUR.add_object("gravel", 2, 1)
move()
take()
move()
put()
move()
```

Note the number 1 appearing at the bottom left, indicating the number of `"gravel"` as an object.  `"gravel"` is normally used as a **background tile** to create more interesting looking worlds... and not as an object to be picked up by Reeborg.

#### Gravel as an object?

As we mentioned, while we can use arbitrary "things" as objects, it might not always make sense.  Then again... Perhaps one could design a world where `take()` is replaced by `shovel()` and Reeborg must shovel out some gravel to clean a path.

