
# Changing the colors

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