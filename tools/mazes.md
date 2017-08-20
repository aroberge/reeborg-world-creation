# Mazes

Mazes can provide interesting examples for various programming puzzles; they can also be used to illustrate various search algorithms.

![](/assets/maze.png)

## Creating simple mazes

If you need to create simple mazes, with a single path randomly generated and one square grid wide which fills the entire world, you can use the following:

```py
RUR.create_maze(7, 7)
```

![](/assets/maze_normal.png)

In the image above, and the one below, I have included the control button for running the program so as to get a better sense of the scale.

Larger grids can be created ... but it may be useful to draw them with smaller grid size to fit them better on the screen.

```py
RUR.create_maze(14, 14, {"small_tiles": True})
```

![](/assets/small_maze.png)

### Maze construction

Mazes are constructed using a depth-first search algorithm adapted from [http://rosettacode.org/wiki/Maze\_generation](http://rosettacode.org/wiki/Maze_generation); using this algorithm results in a simply connected maze, one without any loops or closed circuits, and without any inaccessible areas; this type of maze is sometimes called a "perfect maze".  We can show how a maze is constructed by using the `"recording"` option.

```py
think(100)   # speeding up from default value of 300 ms
RUR.create_maze(10, 10, 
                {"small_tiles": True,
                "recording": True})
```

### ![](/assets/maze_anim1.gif)

First, the world is emptied of all its content and its size is adjusted based on the first two arguments of `RUR.create_maze()`; then, walls are added everywhere possible; they are then removed one by one using a depth-first search algorithm.

To illustrate better the algorithm, we can use colors; a default palette, subject to change, has been used in the illustration below:

```py
think(100)
RUR.create_maze(10, 10, 
                {"small_tiles": True,
                "recording": True,
                "use_colors": True})
```

![](/assets/maze_anim2.gif)

With a world filled with walls:

1. We pick a random cell as our starting point; this is the green square.
2. From our current location:
   1. we pick a neighbouring cell at random, but one that has not been visited; this cell is shown in red
   2. we remove the wall between these two cells., and add the neighbour to the list of visited cells; the previously visited cell is now colored yellow.
   3. we go back to i. until we end up with a cell without any unvisited neighbours; in this case we backtrack to a previous cell that has at least one unvisited neighbour \(leaving the "dead end" cell red\).
   4. we repeat this process until there are no unvisited cell.

There is an additional color choice made above, having nothing to do with the algorithm: when a cell can be reached from three neighbours without walls blocking the way, it is colored in grey; if a cell could be reached by its four neighbours, a different color would be used.

> **\[warning\] Creating your own version**
>
> If you try to implement your own version of this algorithm using Python, you may find that the display will appear to be frozen for a relatively long time as the maze is created.

### Adding rooms

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

## Changing the colors

It is possible to change the "colors" from the default, by specifying a custom palette. We can use either standard colors **or** any known "thing" as a color. Here is an example showing all possible values that can be specified, illustrating how a maze with rooms is constructed:

```py
RUR.create_maze(12, 10, 
    {"use_colors": True,
    "nb_rooms_goal": 4,
    "room_width": 2,
    "room_height": 2,
    "room_max_width": 5,
    "room_max_height": 5,
    "nb_doors_goal": 3,
    "recording": True,
    "palette": {"start": "grass",
        "end": "bricks",
        "two way": "grass",
        "three way": "grass",
        "four way": "grass",
        "in room": "soil"}
        })
```

![](/assets/maze_rooms.gif)

## Getting information about the maze

In a previous section \(add link to "Lists, tuples, dict" section\), I mentioned how one can get a complete "world map". For example, using Python:

```py
gps = SatelliteInfo()  # English version; different names are used in French
gps.print_world_map() # prints a formatted version

# extract information from a dict
gps.world_map["goal"] # extracts the goal information for this world
```

whereas for JavaScript, we have

```js
// Same names in all languages
var goal, map;
RUR.print_world_map();  // prints formatted version

map = RUR.world_map();  // JavaScript Object
goal = map.goal;        // or goal = map["goal"] like in the Python version
```

This "world map" contains all the information required to draw the world. However, the information normally recorded does not allow for an easy identification of regions without walls \(rooms\), or openings leading to these regions, etc.  For this reason, when a maze is created using `RUR.create_maze()`, some additional information is recorded in a more user-friendly format. To see this additional information, you can use `RUR.print_maze()`. If we use it with the maze shown above, with the palette using only `"grass", "bricks", "soil"`, we get the following:

```json
{
  "rooms": [
    {
      "x_min": 8,
      "y_min": 2,
      "x_max": 12,
      "y_max": 4,
      "doors": [
        {
          "direction": "north",
          "x": 10,
          "y": 3
        },
        {
          "direction": "south",
          "x": 10,
          "y": 2
        },
        {
          "direction": "west",
          "x": 8,
          "y": 3
        }
      ]
    },
    {
      "x_min": 9,
      "y_min": 8,
      "x_max": 13,
      "y_max": 11,
      "doors": [
        {
          "direction": "south",
          "x": 11,
          "y": 8
        },
        {
          "direction": "west",
          "x": 9,
          "y": 8
        }
      ]
    },
    {
      "x_min": 1,
      "y_min": 1,
      "x_max": 4,
      "y_max": 5,
      "doors": [
        {
          "direction": "north",
          "x": 3,
          "y": 4
        },
        {
          "direction": "east",
          "x": 3,
          "y": 1
        }
      ]
    },
    {
      "x_min": 1,
      "y_min": 8,
      "x_max": 5,
      "y_max": 10,
      "doors": [
        {
          "direction": "south",
          "x": 3,
          "y": 8
        },
        {
          "direction": "east",
          "x": 4,
          "y": 8
        },
        {
          "direction": "north",
          "x": 3,
          "y": 9
        }
      ]
    }
  ],
  "start": {
    "x": 11,
    "y": 6
  },
  "palette": {
    "start": "grass",
    "two way": "grass",
    "end": "bricks",
    "three way": "grass",
    "four way": "grass",
    "in room": "soil"
  },
  "use_colors": true,
  "nb_rooms_goal": 4,
  "room_width": 2,
  "room_max_width": 5,
  "room_height": 2,
  "room_max_height": 5,
  "nb_doors_goal": 3
}
```

If we wish to obtain information about a particular maze feature, rather than simply printing it, we can easily do so. Here's an example using Python:

```py
gps = SatelliteInfo()
rooms = gps.world_map['maze']['rooms']
print(rooms[0])  # for example
```

and the same example using JavaScript

```js
var rooms;
rooms = RUR.world_map()['maze']['rooms'];
write(rooms[0]);  // for example
```



