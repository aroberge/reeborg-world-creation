# Maze construction algorithm

Mazes are constructed using a depth-first search algorithm adapted from [http://rosettacode.org/wiki/Maze\_generation](http://rosettacode.org/wiki/Maze_generation); using this algorithm results in a simply connected maze, one without any loops or closed circuits, and without any inaccessible areas; this type of maze is sometimes called a "perfect maze".  We can show how a maze is constructed by using the `"recording"` option.

```py
think(100)   # speeding up from default value of 300 ms
RUR.create_maze(10, 10,
                {"small_tiles": True,
                "recording": True})
```

![](/assets/maze_anim1.gif)

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