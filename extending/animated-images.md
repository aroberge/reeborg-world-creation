# Animated images

Worlds can be made much more visually interesting by adding animations. Run the program below. I have inserted two pauses so that you will need to click 3 times on the **run** button to see the entire program.

* At the first pause: look closely at the water and the fire: you will see that the images are changing slightly in a random pattern.
* Look closely when you click on the run button a second time: the box which has been pushed in the fire burns up and the flame temporarily gets bigger.
* After the third time you click on the run button, Reeborg tosses the bucket of water into the flame, extinguishing them in a short animation.

```py
World("Alone")
recording(False)
RUR.add_background_tile("water", 3, 2)
RUR.add_background_tile("fire", 3, 1)
RUR.add_object("bucket", 1, 1)
take()
RUR.add_pushable("box", 2, 1)
recording(True)
RUR.record_frame()

pause()
move()
pause()
toss()
```

To create an animation, a series of different images is associated with a given object; this was already mentioned in the Beepers chapter. Excluding robot animations, which are explained below, all images are animated  at a set interval, which is independent of the animation time use to show each execution step of the program. Because of this, the program \(playback\) can be paused and the animations will continue.

The default time interval between changes of images is 120 ms; this is reset whenever a world is loaded and can be changed for a given world by assigning a value to `RUR.ANIMATION_TIME` in the **Onload **or **Pre **editor; this is a global value and the last setting is the one that applies for the entire program.[^1]

Currently, five different types of animations are supported. This is demonstrated in the world

```py
World("/worlds/examples/animated_all.json", "animated")
```

which you should look at closely to better understand the following description of each type of animation possible.

1. All animated images of a given type cycle through at the same time. This is shown on the bottom row \(`y=2`\) with images of the world where I have chosen to represent all animated tiles in by the same images \(numbers from 1 to 5\). The animation time has been slowed down from the default.  
2. Each animated tile cycle through an orderly fashion, but starts at a random point in a cycle. This is shown on the second bottom row \(`y=4`\). This is the animation type used for beepers.
3. Each animated tile changes randomly at each cycle. This is shown on the `y=6` row. This is the animation type for `water` and `fire`.
4. A single cycle through all the images is done; after it is completed, the last image is shown repeatedly. \(Currently, it is redrawn each time, even when it is not changing\). This is shown on the `y=8` row.
5. A single cycle is done after which the tile/object is removed from the world. This cannot realistically be used for objects which cannot be picked up by the robot.  However, this is the type of animation that has been used in the first example above for the burst of flame and for the flame being doused by water.  

## Animated robots

Robot animation is done independently of other animations; it also uses a different approach.  You may recall the example we have seen on how to add your own robots:

```py
   RUR.new_robot_images({"model": "rat",
    "east": "/src/images/rat_e.png",
    "north": "/src/images/rat_n.png",
    "west": "/src/images/rat_w.png",
    "south": "/src/images/rat_s.png"
    })
```

Each robot is identified by a model number and has four different images, one for each orientation. Animating a robot is done by changing the model number in a cyclical pattern, as shown in the following example:

```py
World("Empty")
reeborg = UsedRobot()
RUR.animate_robot(["classic", "light blue", "yellow"], reeborg.body)
for i in range(8):
    move()
    turn_left()
```

The speed of animation is controlled via the global variable `RUR.ROBOT_ANIMATION_TIME` which has a default value of 150 ms. Like `RUR.ANIMATION_TIME,`this is a global value and the last setting is the one that applies for the entire program. With the default value for the transition between each frame \(300 ms\), we never see the _yellow_ value until the end of the program: each frame starts the animation at the first image. If you want to control completely the animation, you can redefine `think()` to set a specific value and prevent the student from changing the playback speed.

We can, however, change the way a robot is animated in different parts of a program; if we don't specify a `robot.body`, then the default robot is used.

```py
World("Alone")
RUR.ROBOT_ANIMATION_TIME = 250
think(1000)
RUR.animate_robot(["classic", "yellow"])
for i in range(4):
    move()
    turn_left()
RUR.animate_robot(["classic", "light blue"])
```

To indicate that only one animation cycle should be done, ending with the last model, we use the value if `-1` as the last value. For example, one could redefine functions like `move()` or `turn_left()` and design a robot that would go through a series of animations as it moves[^2] so that the robot could be seen "slowly" moving from one square grid to the next, or slowly rotating. Since I do not have appropriate images to illustrate this idea, here's a rough implementation of what it might look like.

```py
World("Alone")
left = turn_left
RUR.ROBOT_ANIMATION_TIME = 150 # this is the default
def turn_left():
    old_delay = think(601) # time to complete 4 animations and switch to 5th model
    RUR.animate_robot(["yellow", "light blue", "yellow", "light blue", "classic", -1])
    think(0)
    left()
    think(old_delay)
    RUR.animate_robot(["classic"])

for i in range(4):
    move()
    move()
    turn_left()
```

[^1]: You may recall that running a program means creating a series of frames which are then displayed one by one. When they are displayed, the value of global variables like `RUR.ANIMATION_TIME` has been set and will not change until a program is stopped and the world reloaded.

[^2]: This may require using robot images larger than a grid square.

