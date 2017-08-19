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



### To do

* Add animation showing maze built
* Explain how to use `RUR.is_wall(direction, x, y)` to find a path and suggest exploration of various algorithms \(depth-first search, breadth-first search, A\*\)
* Document option\(s\) to create other types of mazes.



