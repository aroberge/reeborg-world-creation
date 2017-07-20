# Background tiles, obstacles and decorative objects

While walls can be used to create obstacles in Reeborg's path, using other elements, such as certain background tiles and obstacles can achieve the same purpose while being visually a lot more attractive.

if you are familiar with the menu-driven **World editor**, you will realize that most of the examples given below could be created just as easily using the **World editor**.** **However, the methods we present can be used more generally to create much more interesting worlds, which could not be done by simply using the World editor.

## Preamble

When a user click on the "run" button or the "step" button to execute a program, the entire program gets executed, with a **frame **being recorded whenever the state of the world changes. What is shown is a playback of the recorded frames, shown one by one. This allows for easy stepping through a given program, or even stepping back.

## Background tiles

Adding background tiles can be done as follows:

```py
RUR.add_background_tile("grass", 2, 1)
RUR.add_background_tile("gravel", 3, 1)
```

If you write this code in the main editor and run the program, you will see that each background tile is added one at a time: each time a change occurs in the world, a **frame** is recorded and shown separately. When creating a background, this will likely not be the desired behaviour. Usually, you will want to create backgrounds by writing code in the **Onload **editor; in this case, you will not see tiles added one by one: code executed from the Onload editor does not result in a visible frame-by-frame recording.

However, you might sometimes want to make such addition or transformation of the world while a program is running. In this case, if you do not want to see the additions done one by one, you will have to suspend the recording of changes being made, make multiple changes, and resume the recording so that changes can appear. We can control the recording behaviour with the `recording()` function as shown in the following example which you should try.

```py
previous_recording_state = recording(0)
RUR.add_background_tile("grass", 2, 1)
RUR.add_background_tile("gravel", 3, 1)
recording(previous_recording_state)

pause(1000)
move()
move()
```

`recording` normally expects a boolean variable; it returns the previous recording state. Since I wanted to provide an example which work with both Python and Javascript, I used `0` instead of `False` or `false` which we would usually recommend when showing code to students using a single language. Furthermore, while we know in this example that we want to resume recording, it is a good practice to use the return value to save the previous recording state, and use it in a subsequent call to resume as before.  This can be useful when defining functions that are intended to suspend recording and can be called within other functions that do the same.

Since `pause()` does not change the content of the world, it does not trigger a recording; however, by using it, we can delay showing the next recorded frame which is triggered by a `move()`, so as to show all at once the changes \(2 background tiles added and a new location for Reeborg\).

> French version: _En français, utilisez _`enregistrement()`_ au lieu de _`recording()`_._

If we want to fill the entire world with a single tile, we can use something like the following:

```py
RUR.fill_background("grass")
```

Some background tiles can not only make a world more visually interesting, but they can be used instead of wall to create obstacles. For example, `water` and `mud` are both fatal to Reeborg ... but only one of them \(`water`\) can be detected. Below is a Python program that illustrates this.

```python
previous_recording_state = recording(0)
RUR.add_wall("east", 3, 1)
RUR.add_background_tile("water", 3, 2)
RUR.add_background_tile("mud", 3, 3)
karel = UsedRobot(1, 2)
reeborg = UsedRobot(1, 3)
recording(previous_recording_state)

while front_is_clear():
    move()

while karel.front_is_clear():
    karel.move()

while reeborg.front_is_clear():
    reeborg.move()
```

I have already mentioned `RUR.show_all_things()`before. To see which "things" included that are fatal, use an optional argument:`RUR.show_all_things("fatal")`; to see those that can be detected by Reeborg, use `RUR.show_all_things("detectable")`. As we have seen in the previous program, some things, like `water` are both fatal and detectable, whereas others \(namely `mud`\) are fatal but not detectable. There are also others \(like `house`, use as a final destination\) which are detectable but not fatal. As you will see later, it is possible to add your own "things" with your own choice of default properties.

## Obstacles

Obstacles are visual elements, usually `fatal`, which are drawn on top of the background tile layer, no matter which in which order the various "things" are added.  For example, the program

```py
RUR.add_background_tile("grass", 2, 1)
RUR.add_obstacle("fence_left", 2, 1)
RUR.add_obstacle("fence_right", 3, 1)
RUR.add_background_tile("grass", 3, 1)
```

will result in the following

![](/assets/background4.png)

## Decorative objects

Decorative objects are simply drawn for visual effects: by default, they cannot affect any interaction that Reeborg could have. As we have seen for objects that can be picked up by Reeborg, they appear together with a number indicating how many such objects are present at a given location. By contrast, decorative objects are shown by themselves, with no such number indicated.

![](/assets/background5.png)

Visually, decorative objects appear between obstacles and background tiles, while objects \(that can be picked up\) appear on top of obstacles and background tiles.

![](/assets/background6.png)

By default, it would make little sense to put objects that need to be picked up on top of obstacles since Reeborg could never reach them. However, one could create worlds where obstacles would disappear if Reeborg were to accomplish a given sub-task first.

## Beyond the menu-driven World editor

The menu-driven World editor limits choices as to what can be drawn as a background tile, an obstacle, a decorative object, etc. Using the API, one is not limited. As a possible interesting example, one can imagine drawing a "river" with consecutive `water` tiles as background tile except at one location where we draw it as a decorative object. Visually, it would appear to be the same everywhere. However, as a decorative object, `water` would be harmless so that Reeborg could cross it safely. One could make a story about finding the point where the river is shallow enough for Reeborg to cross it. This could be done by Reeborg using either `front_is_clear()` or `right_is_clear()`. For demonstration purpose I have created two versions of a world that demonstrate this idea. The first version is the one that I would use with students:

```py
World("worlds/examples/river_demo.json", "Crossing the river")
```

Load this world, then click on **World Info** to see how it is done.

In the second version, I do not draw the safe river passage in the **Onload **editor, but do so in the **Pre **editor instead. This way, one can see before running the program where the passage will be.

```python
World("worlds/examples/river.json", "River")
```

Again, click on **World Info** to see how it is done as I used a very special trick.  When a program is run from the Onload editor, it is run in its own context/scope: any variable defined in this context is not going to be shared with the user's program. In order to make a variable available globally, I use a special Javascript object / Python dict to store the value and to retrieve it when needed.

