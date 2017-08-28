# Breadth-first search

> **\[danger\] The version on the website may not be compatible with the code presented here.**
>
> This will be fixed in the near future.

In the previous section, we used a breadth-first search algorithm to visit an entire world. This is not particularly useful. A better use case is for finding a path between two nodes, which we call **start** and **goal**. All that is required is to add a test to see if we have found the goal, and quit at that point.  To make the code clearer, we encapsulate the algorithm in a function.

```py
from search_tools import Deque, get_neighbours
World("Empty")
think(0)
no_highlight()

def find_goal_bfs(start, goal):
    '''Starting from the *start* node, uses a breadth-first search
       algorithm to explore a world until the *goal* node is found.
    '''
    frontier = Deque()
    frontier.append(start)
    visited = set([start])

    while not frontier.is_empty():
        current = frontier.get_first()

        if current == goal: # <-- new test added
            return        

        for neighbour in get_neighbours(current):
            if neighbour not in visited:
                frontier.append(neighbour)
                visited.add(neighbour)

                #  Test here?

        frontier.mark_done(current)

# set up
RUR.set_world_size(10, 10)
start = 3, 3
goal = 6, 4
RUR.add_object("star", *goal)
find_goal_bfs(start, goal)
```

Instead of checking if we have reached the goal when we select a node from the frontier, we could do it when we add a **neighbour** to the set of visited nodes. This would work here but would be guaranteed to yield the best possible path when we introduce a cost function later on.

## Getting the path

So far the algorithm as implemented explores the world until the goal is found, but it does not give a path to follow. This can be remedied by a simple change.  As usual, we follow fairly closely the notation from [Red Blob Games](http://www.redblobgames.com/pathfinding/a-star/introduction.html).

Instead of using a set for recording the visited nodes, we use a dict whose keys are nodes and corresponding values are nodes that were immediately visited before; we call this dict `came_from`, and note the relevant line changes below by the comments labeled 1a, 1b, and 1c.  We also add the option of not using colour to show the visited nodes \(comments 2a and 2b\). Finally, we return the `came_from` dict \(comment 3\).

```py
def find_goal_bfs(start, goal, no_colors=False): # 2a
    '''Starting from the *start* node, uses a breadth-first search
       algorithm to explore a world until the *goal* node is found,
       recording the nodes visited along the way.
    '''
    frontier = Deque(no_colors=no_colors)  # 2b
    frontier.append(start)
    came_from = {start: None}  # 1a

    while not frontier.is_empty():
        current = frontier.get_first()
        if current == goal:
            return came_from  # 3

        for neighbour in get_neighbours(current):
            if neighbour not in came_from:  # 1b
                frontier.append(neighbour)
                came_from[neighbour] = current # 1c
        frontier.mark_done(current)
```

The path can be reconstructed using the `came_from` dict as follows:

```py
current = goal
path = [current]
while current != start:
    current = came_from[current]
    path.append(current)
```

And here's a full program that can find a path, and show it in colours at the end.

```py
from search_tools import Deque, get_neighbours
World("Empty")
think(0)
no_highlight()

def find_goal_bfs(start, goal, no_colors=False):
    '''Starting from the *start* node, uses a breadth-first search
       algorithm to explore a world until the *goal* node is found,
       recording the nodes visited along the way.
    '''
    frontier = Deque(no_colors=no_colors)
    frontier.append(start)
    came_from = {start: None}

    while not frontier.is_empty():
        current = frontier.get_first()
        if current == goal:
            return came_from

        for neighbour in get_neighbours(current):
            if neighbour not in came_from:
                frontier.append(neighbour)
                came_from[neighbour] = current
                if neighbour == goal:
                    return came_from
        frontier.mark_done(current)

# set-up
RUR.set_world_size(10, 10)
goal = 9, 9
start = 3, 3
RUR.add_object("star", *goal)
reeborg = UsedRobot(*start)
reeborg.set_model("yellow")

# do the search; do not use colors to indicate the search
# so that we can focus on the final result
came_from = find_goal_bfs(start, goal, no_colors=True)

# obtain path from search result
current = goal
path = [current]
while current != start:
    current = came_from[current]
    path.append(current)

# draw the path
for node in path:
    RUR.add_colored_tile("green", *node)
```

Since we select the neighbours of a given node in a random order by default, the path found may vary each time the program is executed. Here's one possible final result:

![](/assets/bfs_path.png)

## Make Reeborg follow the path

Add explanation here.

We replace

```py
# draw the path
for node in path:
    RUR.add_colored_tile("green", *node)
```

by

```py
path.reverse()
del path[0]  # Reeborg is there already

for node in path:
    while node != reeborg.position_in_front():
        reeborg.turn_left()
    reeborg.move()
```

Below is an image showing the final result. In addition to the above changes, we have also:

* removed `reeborg.set_model("yellow")`, to use the default robot model;
* replaced `RUR.add_object("star", *goal)` by `RUR.add_final_position("house", *goal)` so that there would be an automatic verification done at the end, confirming that we have reached the goal.

![](/assets/bfs_path3.png)

> **\[info\] Observation**
>
> Although all paths found will the same number of `move()` instructions required to reach the goal, most of them will require many extra `turn_left()` instructions and thus will not be the most efficient from Reeborg's point of view.



