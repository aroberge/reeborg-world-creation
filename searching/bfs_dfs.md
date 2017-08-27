# Breadth-first and depth-first algorithms

Both algorithms follow the same pattern:

* Start at a node, which is the **frontier**, i.e. how far we have visited so far
* Repeat until all nodes have been visited:
  * Pick and remove a node from the **frontier**
  * Add this node to the ones that have been visited
  * Get this node's neighbours; any of them that have not been visited is added to the **frontier**

Visually, the beginning looks as follows:

![](/assets/bfs.png)

1. We add a node to the frontier \(node color is light blue\)
2. We retrieve a node added to the frontier \(we have only one to choose from\) and set it as the current node \(green\)
3. a, b, c, d\) we add the neighbours of the current node to the frontier.
4. Having found all the neighbours, we add the original node to the visited ones \(colour changed to light grey\)
5. We retrieve a node from the frontier \(in this case, we picked the last one that was added\)
6. a\) We add its first neighbour to the frontier; etc.

Using Python, the general algorithm looks as follows:

```py
start = (x, y)
frontier.append(start)
visited[start] = True

while not frontier.is_empty():
    current = frontier.GET_NODE()
    for neighbour in GET_NEIGHBOURS(current):
        if neighbour not in visited:
            frontier.append(neighbour)
            visited[neighbour] = True
```

If `GET_NODE()` is retrieving the **first** node that was added to the frontier \(First In, First Out, or FIFO\), we have a breadth-first algorithm  If `GET_NODE()` is retrieving the **last** node added to the frontier \(Last In, First Out, or LIFO\), we have something similar to a depth-first algorithm. \(A true depth-first algorithm would label a node as visited only when it is retrieved from the frontier.\)

For `GET_NEIGHBOURS()` we'll consider two cases: either we get them always in the same order, or we get them in a random order each time.

The data structure I will use for the frontier is a double ended queue or deque. I have implemented a custom deque, not as efficient as the one included in the Python standard library but one that does take care of indicating which node is visited using colours, without cluttering unduly the user's code.

> **\[info\]** Using a proper data structure
>
> Deque and PriorityQueue \(to be introduced later\) should not be used when trying to write efficient code. Students should be taught to use proper data structures when writing their own code.

For the visited nodes, we could have used a Python set instead of a dict; however, when we will actually use the algorithm to search for the shortest path, a set will not be sufficient, and using a dict right now will minimize the changes.

Let's first look at the cases where we select neighbours always **in the same order**. A complete program to do this for breadth-first search is as follows:

```py
from search_tools import Deque, get_neighbours

no_highlight()  # highlighting would create too many frames
                # however, for smaller worlds, you might want to leave it on and
                # step through the program

think(0)        # Makes display update as fast as possible
World("Empty")
RUR.set_world_size(11, 11)

frontier = Deque()
visited = {}

start = (6, 6)
frontier.append(start)
visited[start] = True

while not frontier.is_empty():
    current = frontier.get_first()  # <-- See comment below
    for neighbour in get_neighbours(current, ordered=True):
        if neighbour not in visited:
            frontier.append(neighbour)
            visited[neighbour] = True
    frontier.mark_done(current)  # changing color only
```

To change from breadth-first to our quasi-depth-first, we simply need to change `frontier.get_first()` to `frontier.get_last()`.

Below is a comparison of the two different algorithms,. On the left, we are using breadth-first: the frontier is expanding uniformly  
away from the center. For both of these, we have made a world with small tiles using `RUR.get_current_world().small_tiles = True` after selecting `World("Empty")`.

![](/assets/bfs_dfs_ordered.gif)

If we choose the neighbours in random order, by removing `ordered=True`, we get the following:

![](/assets/bfs_dfs.gif)

The breadth-first case does not look significantly different; however, the other case definitely does. A recursive version of a proper depth-first search algorithm with randomly ordered neighbours is what the `RUR.create_maze()` function uses.

