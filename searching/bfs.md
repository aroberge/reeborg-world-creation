# Breadth-first search

Encapsulate in a function

```py
from search_tools import Deque, get_neighbours
World("Empty")
think(0)
no_highlight()

def find_goal_bfs(start, goal):
    '''Starting from the 'start' node, uses a breadth-first search
       algorithm to explore a world until the 'goal' node is found.
    '''
    frontier = Deque()
    frontier.append(start)
    visited = set([start])

    while not frontier.is_empty():
        current = frontier.get_first()
        for neighbour in get_neighbours(current):
            if neighbour not in visited:
                frontier.append(neighbour)
                visited.add(neighbour)
                if neighbour == goal:     # <--
                    return
        frontier.mark_done(current)

# set up
RUR.set_world_size(10, 10)
goal = 6, 4
RUR.add_object("star", *goal)
find_goal_bfs((3, 3), goal)
```

## Getting the path

```py

def find_goal_bfs(start, goal, no_colors=False): # 0
    '''Starting from the 'start' node, uses a breadth-first search
       algorithm to explore a world until the 'goal' node is found,
       recording the nodes visited along the way.
    '''
    frontier = Deque(no_colors=no_colors)
    frontier.append(start)
    came_from = {start: None}  # 1a

    while not frontier.is_empty():
        current = frontier.get_first()
        for neighbour in get_neighbours(current):
            if neighbour not in came_from:  # 1b
                frontier.append(neighbour)
                came_from[neighbour] = current # 1c
                if neighbour == goal:
                    return came_from # 2
        frontier.mark_done(current)
```

To obtain the path, here's what we do
```py
current = goal
path = [current]
while current != start:
    current = came_from[current]
    path.append(current)
```

And here's a full program to use this

```py
from search_tools import Deque, get_neighbours
World("Empty")
think(0)
no_highlight()

def find_goal_bfs(start, goal, no_colors=False):
    '''Starting from the 'start' node, uses a breadth-first search
       algorithm to explore a world until the 'goal' node is found,
       recording the nodes visited along the way.
    '''
    frontier = Deque(no_colors=no_colors)
    frontier.append(start)
    came_from = {start: None}

    while not frontier.is_empty():
        current = frontier.get_first()
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
for cell in path:
    RUR.add_colored_tile("green", *cell)
```

## Make Reeborg follow the path

Add explanation here.