# Adding rooms

In some games, it is useful to have rooms connected by mazes. We can add rooms to mazes using an option as follows:

```py
RUR.create_maze(12, 10,
                {"small_tiles": True,
                "use_colors": True,
                "nb_rooms_goal": 5,
                "room_width": 4})
```

Rooms are positioned randomly, with at least one grid gap between each room. If the required area to draw all rooms were to exceed the total available area, an error would be raised.  If not, an attempt is made to fit as many rooms as possible up to the maximum value; the reason why the number of room specified has the word `goal` in it is as a reminder that the maze created might not have that many rooms in it.  One can specify either the `width` or the `height` or both for the rooms to be created. If no value is specified, a default value of 1 is used. For example, the code above was used to generate the following maze:

![](/assets/maze_rooms1.png)

Here is another example:

```py
RUR.create_maze(12, 10,
                {"use_colors": True,
                "nb_rooms_goal": 5,
                "room_width": 4,
                "room_height": 3})
```

![](/assets/maze_rooms2.png)

In this second example, we can see that fewer rooms were created than the stated goal.  In both of these examples, the rooms were created without doors. Furthermore, the grid pattern is not visible within the rooms: the default "color" used was the pattern used to represent `gravel` which is opaque, unlike the other colors that were used by default.  We can make the grid visible **and** add doors to the rooms as follows:

```py
RUR.create_maze(12, 10,
                {"use_colors": True,
                "nb_rooms_goal": 5,
                "room_width": 4,
                "room_height": 3,
                "nb_doors_goal": 3,    # <--
                "visible_grid": True   # <--
                })
```

![](/assets/maze_rooms3.png)

For a given side of a room, there can only be one door, and there cannot be any door on the boundary of the world: this explains why the room at the bottom left has only two doors.  Note the purple grid square: this is the default color for a grid square that is accessible from any of its four neighbours.

Having room with fixed sizes might be too boring; it is possible to specify a larger **maximum** value for each of the width and height parameter for the rooms:

```py
RUR.create_maze(12, 10,
                {"use_colors": True,
                "nb_rooms_goal": 4,
                "room_width": 2,
                "room_height": 2,
                "room_max_width": 5,   # <--
                "room_max_height": 5,  # <--
                "nb_doors_goal": 3,
                "visible_grid": True})
```

![](/assets/maze_rooms4.png)