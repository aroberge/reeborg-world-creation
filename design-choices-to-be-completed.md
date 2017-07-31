# Design choices

After using Reeborg's World for a while or reading the world creation API documentation, you might be puzzled as to some design choices I have made. In this appendix, I attempt to explain the reasoning behind some choices I made.

## Silencing some errors

One of my frustrations when writing Javascript code is that sometimes, especially if using third-party libraries, errors/exceptions being raised are silenced. Usually, I much prefer the norm in Python where errors/exceptions have to be dealt with explicitly by the user.  However, from my own experience in working with the API for creating worlds, I found that dealing with certain types of errors brings very little clarity and much frustration.  Inspired from the Zen of Python:

```
...
Errors should never pass silently.
Unless explicitly silenced.
...
```

I have decided that some errors should be always silenced, while others should be silenced depending on context.  On this last point, in particular, if a world is created with code from the **Onload **editor, like:

```
RUR.add_bridge("bridge", 2, 2)
```

a bridge will be added to the world's content when the world is imported.  If this world is then saved \(perhaps after some editing done\), there will be a bridge included in the new world definition.  When this new world is imported, the Onload code will be executed ... and since there can only be one bridge at a given location, an error would normally be raised immediately.  Most world creators would not be able to find the source of that error easily ... and once they would have found it, they might be frustrated at having to either explicitly edit the json world file using a text editor, or alter some code in the Onload editor \(which is not executed when editing a world\).

#### Background tiles

There can only be one background tile per location. Rather than requiring to first remove an existing background tile, and then add a new one, when a new one is to be added using

```py
RUR.add_background_tile("name", x, y)
```

it simply replaces any pre-existing tile at that location.  To help prevent typos, if `"name"` is not recognized as a valid artefact, an error is raised.  However, one can also create uniformly colored tiles to used as a background tile: any color notation recognized by JS/HTML is available for this. This is done using

```py
RUR.add_colored_tile("color", x, y)
```

Again, this replaces any pre-existing tile; however, this time `"color"` must **not **be a known artefact otherwise an error will be raised.

To fill the entire background tiles with a single type we use

```py
RUR.fill_background("type", x, y)
```

where `"type"` can be either a known artefact or a color: not check is performed.

**Note**: if the "color" is not recognized as valid by JS/HTML, it will be painted black.

#### Bridges

As mentioned above, attempting to add a bridge where one already exists \(even if it is the same type\) will raise an error except if this is done from the Onload editor, in which case a message will simply be logged in the browser's console.

#### Decorative objects

Decorative objects are of no consequence for the behaviour of a program. If one tries to add a second decorative object of a given type \(for example, a tulip\) at a given location, the request will be silently ignored.  Note that this could result in an error later if one attempts to remove a given type of decorative object twice at the same location.

#### Objects

By "objects", I mean those that Reeborg can `take()` and `put()`.

New error handling to be implemented and documented better: in the Onload editor, "adding" an object will be seen as identical to "set".

#### Obstacles

Multiple obstacles can exist at a given location. However, attempting to add a named obstacle where one already exists with the same name will raise an error except if this is done from the Onload editor, in which case a message will simply be logged in the browser's console.

#### Overlays

```js
raise NotImplementedError
```

Overlays do not exist yet. When they are, they should be handled somewhat similarly to decorative objects.

#### Pushables

New error handling to be implemented. Should be handled somewhat similarly to bridges.

#### Walls

New error handling to be implemented. Should be handled somewhat similarly to bridges.

## Editor content cannot be changed when using Blockly

To be explained

## Why having both obstacles and background tiles?

While both obstacles and background tiles can be "fatal", having both enables a world creator to combine images and make the world more visually appealing. For example, we can have fire as an obstacle on an otherwise harmless grass background. The alternative would be to combine fire and grass into a single image to be used as a fatal element. Such an approach could lead to an exponentially growing number of images having to be created.

