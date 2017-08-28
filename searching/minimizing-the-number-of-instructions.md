# Minimizing the number of instructions

As we have seen, using breadth-first search, we can find a shortest path between two points; however, the path found is not necessarily the most efficient one for Reeborg.

When it comes to moving from one point to another in the world, Reeborg uses two instructions: `move()` and `turn_left()`. An efficient path is one that minimizes the number of such instructions.  We can easily adapt our algorithm to find the most efficient path. Let's review what happens when we use these two instructions:

* A `move()` instruction takes Reeborg from location `(x, y)` to location `(x', y')` which are next to each other on a grid. For example, if Reeborg is facing `east`, we will have `x' == x + 1` and `y' == y`.
* A `turn_left()` instruction leaves Reeborg at the same location `(x, y)`, but makes its direction change.

We can encode this information by using a graph with a different definition of nodes: a node will include both coordinates `x` and `y` as well as the direction in which Reeborg is facing.  For example, `(2, 3, "east")` could be a node. For this type of graph, nodes are 3-tuples whereas before we had 2-tuples. As it turns out, we can find its neighbours using the same function as before, but calling it with an optional parameter set to `True`.

```py
from search_tools import get_neighbours
neighbours = get_neighbours((2, 3, "east"), directions=True)
print(neighbours)
# If the world is empty, the result will be: 
# [(3, 3, "east"), (2, 3, "north")]
```

```py
from search_tools import Deque, get_neighbours
World("Empty")
think(0)
no_highlight()

def find_goal_bfs(start, goal, no_colors=False, directions=False):
    frontier = Deque(no_colors=no_colors)
    frontier.append(start)
    came_from = {start: None}

    while not frontier.is_empty():
        current = frontier.get_first()
        if (current[0], current[1]) == (goal[0], goal[1]):
            return came_from, current
        for neighbour in get_neighbours(current, directions=directions):
            if neighbour not in came_from:
                frontier.append(neighbour)
                came_from[neighbour] = current
        frontier.mark_done(current)

# set-up
RUR.set_world_size(10, 10)
goal = 9, 9
start = 3, 3, "east"
RUR.add_final_position("house", *goal)
reeborg = UsedRobot(*start)
came_from, current = find_goal_bfs(start, goal, no_colors=True, directions=True)

# obtain path from search result
path = [current]
while current != start:
    current = came_from[current]
    path.append(current)

path.reverse()
del path[0]

def facing(robot):
    directions = [(RUR.EAST, "east"),
                  (RUR.NORTH, "north"),
                  (RUR.WEST, "west"),
                  (RUR.SOUTH, "south")]
    for D, d in directions:
        if robot.body._orientation == D:
            return d

for node in path:
    _, _, direction = node
    if direction != facing(reeborg):
        reeborg.turn_left()
    else:
        reeborg.move()
    
```



