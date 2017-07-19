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



To create an animation, a series of different images is associated with a given object. Excluding robot animations, which are explained below, all images are animated \(i.e. the image shown changes\) at a set interval, which is independent of the animation time use to show each execution step of the program; thus, the program \(playback\) can be paused and the animations will continue.

  
The default time interval between changes of images is 120 ms; this is reset whenever a world is loaded and can be changed for a given world by assigning a value to `RUR.ANIMATION_TIME` in the **Onload **or **Pre **editor; this value is a global value and the last setting is the one that applies for the entire program.

Currently, 5 different types of animations are supported. This is demonstrated in the world

```py
World("/worlds/examples/animated_all.json", "animated")
```

which you should look at closely to better understand the following description of each type of animation possible.

1. All animated images of a given type cycle through at the same time. This is shown on the bottom row \(`y=2`\) with images of the world where I have chosen to represent all animated tiles in by the same images \(numbers from 1 to 5\). The animation time has been slowed down from the default.  This is the animation type for `water` and `fire`.
2. Each animated tile cycle through an orderly fashion, but starts at a random point in a cycle. This is shown on the second bottom row \(`y=4`\).
3. Each animated tile changes randomly at each cycle. This is shown on the `y=6` row.
4. A single cycle through all the images is done; after it is completed, the last image is shown repeatedly. \(Currently, it is redrawn each time, even when it is not changing\). This is shown on the `y=8` row.
5. A single cycle is done after which the tile/object is removed from the world. This cannot realistically be used for objects which cannot be picked up by the robot.  However, this is the type of animation that has been used in the first example above for the burst of flame and for the flame being doused by water.  

## Add section on animated robots



