# Adding your own robots and artefacts

> Vincent Maille and his two co-authors wrote a French book titled [Les robots](https://www.amazon.ca/Robots-Apprendre-Robotique-Par-lExemple/dp/2340013984/ref=sr_1_1?ie=UTF8&qid=1500382251&sr=8-1&keywords=les+robots+maille) which explains how to use Reeborg's World as well as Arduino and Lego Mindstorms robots. He suggested various enhancement to Reeborg's World and created an interesting world which I changed slightly to use as an example for this chapter.

With Reeborg's World, you can add your own images for robots and other objects, or reuse the existing images to create artefacts showing a different behaviour. To see this, you might want to load the following world and click on **World Info** for details.

```py
World("worlds/examples/cheese.json", "Eat cheese")
```

In this world, we have a rat ![](/assets/rat_e.png) that must eat cheese ![](/assets/fromage.png) while avoiding poison ![](/assets/poison.png).  The dimensions of the world are changing each time the world is \(re\)loaded; so is the number of cheese pieces, poison, their positions and that of the rat.

**Note**: if you click on World Info and look at the **Onload** code, there is something that will not be shown, as explained below.

## Adding a robot

To add a robot, we must specify the source of images for each directions \(East, North, South, West\) as well as a model name; if the model name is missing, it will be set to `"anonymous"`; if an image is missing, the default robot image for that orientation will be used.

```py
RUR.new_robot_images({"model":"rat",
    "east": "/src/images/rat_e.png",
    "north": "/src/images/rat_n.png",
    "west": "/src/images/rat_w.png",
    "south": "/src/images/rat_s.png"
    })
```

In the example above, we specified images found on the Reeborg's World site; use the full URL for images found on some other site.

## Adding new things

There are many different options possible when adding new things. At the very least, we must provide a name to use.

```py
RUR.add_new_thing({"name": "cheese",
    "url": "/src/images/fromage.png",
    "info": "Safe to eat."})
```

A single image is specified by the `url` attribute. \(We can have animated images, as explained later\). The `info` attribute is used to get information displayed when clicking on **World Info**.

```py
RUR.add_new_thing({"name": "poison",
    "url": "/src/images/poison.png",
    "fatal": "poison",
    "info": "Do not eat",
    "message": "Gluttony is a terrible thing.<br><img src='/src/images/mort.png'>"
})
```

If the `fatal` attribute is specified \(and not set to `false`\) it will be used in some contexts to raise an exception. For _things_ used as _objects_, this happens when one attempts to `take()` the object. For background tiles or obstacles, this happens when an attempt is made to move at that location.

The `message` attribute is used to show a custom error message when a fatal condition is encountered.  Look closely at the value for this attribute above: it includes the code to insert an image.  However, if you look at the code displayed by the **World Info** for the **Onload** editor, this code will not be shown: the img tag is simply hidden by the CodeMirror syntax highlighter I use.

#### New object goals

In the Cheese example, we did not require the user to put down objects at a specific location; in other words, we did not have goals for objects. If that would have been the case, we would have needed to specify an additional image \(or images\) to use for the goal.  See \[**TODO**: add link\] for more details.

## Custom Errors

When using Python, you can use `ReeborgError` to signal a problem with the code and `ReeborgOK` to give a custom message when everything has been done to meet the goal you have set.

```py
if carries_object("cheese") != RUR.private_dict["nb_cheese"]:
    raise ReeborgError("Some cheese was left behind!")

raise ReeborgOK("All the cheese has been eaten !")
```

If you are using Javascript, you must prepend `RUR.`  as in `RUR.ReeborgError`.

