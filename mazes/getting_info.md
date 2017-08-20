# Getting information about the maze

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

This "world map" contains all the information required to draw the world. However, the information normally recorded does not allow for an easy identification of regions without walls \(rooms\), or openings leading to these regions, etc.  For this reason, when a maze is created using `RUR.create_maze()`, some additional information is recorded in a more user-friendly format. To see this additional information, you can use `RUR.print_maze()`.

![](/assets/maze_rooms.gif)

If we use it with the maze shown above, we get the following:

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

As an example, this information can be used to place objects to be found by the robot inside rooms, avoiding maze passages.

