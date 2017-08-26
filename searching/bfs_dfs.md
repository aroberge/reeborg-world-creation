# Breadth-first and depth-first search


Both algorithms follow the same pattern:

* Start at a node, which is the **frontier**, i.e. how far we have visited so far
* Repeat until all nodes have been visited:
  - Pick and remove a node from the frontier
  - Add this node to the ones that have been visited
  - Get this node's neighbours; any of them that have not been visited is added to the frontier

Using Python, this looks as follows:

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

If `GET_NODE()` is retrieving the **last** node added to the frontier, we have
a depth-first algorithm (also sometimes described as FILO: First In, Last Out).
If `GET_NODE()` is retrieving the **first** node that was added to the frontier,
we have a breadth-first algorithm (also sometimes described as FIFO: First In,
First Out)

For `GET_NEIGHBOURS()` we'll consider two cases: either we get them always
in the same order, or we get them in a random order each time.

The data structure I will use for the frontier is a double ended queue or deque.
I have implemented a custom one, not as efficient as the one included in
the Python standard library but one that does take care of indicating which
node is visited using colours.

For the visited nodes, we could have used a Python set instead of a dict;
however, when we will actually use the algorithm to search for the shortest
path, a set will not be sufficient.

Let's first look at the cases where we select neighbours always in the same
order. A complete program to do this for breadth-first search is as follows:

```py
from search_tools import Deque, get_neighbours

no_highlight()  # highlighting would create too many frames
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

To change to depth-first, we simply need to change
`frontier.get_first()` to `frontier.get_last()`.

Below is a comparison of the two different algorithms. On the
left, we are using breadth-first: the frontier is expanding uniformly
away from the center. On the right, we are using depth-first.
For both of these, we have made a world with small tiles using
`RUR.get_current_world().small_tiles = True` after selecting
`World("Empty")`.
