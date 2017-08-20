# Deleting information about the maze

As a teacher of advanced students, you might want for them to use some search algorithm to find information about a maze, and prevent them from using the special information available. If that is the case, you can use the `RUR.delete_maze_info()` function. If it is called without any argument, it simply deletes all of the available information about a maze; that is, it removes the `maze` entry from `world_map()`. If you want to selectively remove information, you can pass the relevant keywords.

As an example, if we take the maze of the previous section, and execute:

```js
RUR.delete_maze_info("rooms", "palette")
RUR.print_maze();
```

the result will be

```js
{
  "start": {
    "x": 11,
    "y": 6
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

The content associated with any "top-level" key can be deleted this way.



