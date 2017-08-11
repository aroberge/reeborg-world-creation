# Mazes

If you need to create simple mazes, with a single path randomly generated and one square grid wide, fills the entire world, you can use the following:

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

