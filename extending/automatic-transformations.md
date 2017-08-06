# Automatic transformations

**This section is just a rough draft.**

In Reeborg's World, some artefacts can be pushed, some can be tossed \(thrown on the square in front of Reeborg\), and some can be put down by Reeborg. When this happens, depending on the particular artefact and the content of the grid square where it ends up, some automatic transitions can take place:

* A box pushed by Reeborg onto a water background tile becomes a bridge allowing Reeborg to move safely onto that tile.
* A box pushed onto a mud background tile becomes a bridge.
* A box pushed onto a fire background tile will burst into flames and disappear.
* A box pushed onto a fire obstacle will burst into flames and disappear.
* A bucket tossed onto a fire will extinguish the fire.
* A bucket tossed onto a tile with a seed as an object will disappear and the seed will become a tulip.
* A bucket put down on a tile with a seed as an object will disappear and the seed will become a tulip.

All of these are transformations which, currently, are not used in any meaningful way for any programming task, but were implemented as proof of concept to make it easy for you to create your own transformations.

### Achieving similar effects

I will first describe how you might implement this by writing explicit code.  Imagine the situation where Reeborg is facing a box used as a pushable object; behind the box is a water obstacle.  When Reeborg moves, we want the box, which will be pushed onto the water, to transform into a standard bridge, offering protection against water fatality.  Here's what the code required might look like.

```py
# suspend the recording to have everything appearing as one single step
recording_state = recording(False)
move()
x, y = position_in_front()

# conditions at this location
if (   RUR.is_pushable("box", x, y) and
       RUR.is_obstacle("water", x, y) and
       not RUR.is_bridge("bridge", x, y)
    ):
    # actions to perform at the same location
    RUR.remove_pushable("box", x, y)
    RUR.add_bridge("bridge", x, y)

recording(recording_state)
RUR.record_frame()
```

where I have put the three required conditions for the `if` statement on separate lines for reason that should soon become clear. To use this code, you might want to redefine `move` in the **Pre **editor:

```py
def redefine(fn):
    def wrapper(fn):
        recording_state = recording(False)
        fn()
        x, y = position_in_front()
        if (    RUR.is_pushable("box", x, y) and
                RUR.is_obstacle("water", x, y) and
                not RUR.is_bridge("bridge", x, y)
            ):
            RUR.remove_pushable("box", x, y)
            RUR.add_bridge("bridge", x, y)
        recording(recording_state)
        RUR.record_frame()
    return wrapper

move = redefine(move)
```

This would have to be done in the Pre editor in each world where you want this behaviour. Notice that everything is happening always at the same `x, y` coordinate.  In programming, when something is repeated, it often signals that there might be a way to do things more simply, and avoid such repetitions.

Suppose you wanted to use a different image of a box and have it behave similarly.  You might think that you would have to add in a code similar to the above each time. However, this is not the case.  Here's how you could do it.

```py
new_thing = {'name': 'new_box',
    'url': 'some_url_for_the_image',
    'transform' : [
        {'conditions': [ [RUR.is_background_tile, "water"],
                         [RUR.is_pushable, "new_box"],
                         [RUR.is_bridge, "bridge", "not"]
                       ],
         'actions:' [ [RUR.remove_pushable, "newbox"],
                      [RUR.add_bridge, "bridge"]
                    ]
        } # ,{...}
    ]
}
```

If you compare with the first code example, you will see that the `transform` attribute captures the essence of the first code sample above.  Whenever an object or pushable is added to a grid location, an automatic evaluation is done to find out if it has a `transform` attribute; if it does, the conditions listed are evaluated; if they are met, the corresponding actions are performed.

note that `transform` is an array: there can be multiple sets of conditions/actions that are listed in this array.

If you create a **world collection**, you only have to add such objects when creating the menu ... and they will be available in all worlds used, without having to redefine `move()`, `toss()` or `put()`: Reeborg's World will take care of that for you.

