# Greedy algorithm

Add some explanation.

```py
from search_tools import (PriorityQueue,
                          manhattan_distance,
                          Graph)
think(0)
RUR.set_world_size(14, 12)
frontier = PriorityQueue()
start = 3, 3
goal = 12, 10
RUR.add_object("token", *start)
RUR.add_object("star", *goal)

frontier.add(start, 0)
graph = Graph()
came_from = {}

came_from[start] = None

while not frontier.is_empty():
   current = frontier.get_best()

   if current == goal:
      break

   for neighbour in graph.neighbours(current):
      if neighbour not in came_from:
         priority = manhattan_distance(goal, neighbour)
         frontier.add(neighbour, priority)
         came_from[neighbour] = current
   frontier.mark_done(current)

pause()
```

Add screen capture; repeat search multiple times.

With obstacle

```py
from search_tools import (PriorityQueue,
                          manhattan_distance,
                          Graph,
                          reconstruct_path)
think(0)
RUR.set_world_size(14, 12)
frontier = PriorityQueue()
start = 3, 3
goal = 12, 10

recording(False)
for x in range(4, 11):
    RUR.add_background_tile("bricks", x, 11)
    RUR.add_background_tile("bricks", x, 2)
for y in range(3, 11):
    RUR.add_background_tile("bricks", 10, y)
recording(True)


RUR.add_object("token", *start)
RUR.add_object("star", *goal)


frontier.add(start, 0)
graph = Graph()
came_from = {}

came_from[start] = None

while not frontier.is_empty():
   current = frontier.get_best()

   if current == goal:
      break

   for neighbour in graph.neighbours(current):
      if neighbour not in came_from:
         priority = manhattan_distance(goal, neighbour)
         frontier.add(neighbour, priority)
         came_from[neighbour] = current
   frontier.mark_done(current)

path = reconstruct_path(came_from, start, current)
for node in path:
    RUR.add_colored_tile("green", *node)

pause()
```

Compare with breadth first search

```py
from search_tools import (find_goal_bfs,
                          Graph,
                          reconstruct_path)
think(0)
RUR.set_world_size(14, 12)

start = 3, 3
goal = 12, 10

recording(False)
for x in range(4, 11):
    RUR.add_background_tile("bricks", x, 11)
    RUR.add_background_tile("bricks", x, 2)
for y in range(3, 11):
    RUR.add_background_tile("bricks", 10, y)
recording(True)


RUR.add_object("token", *start)
RUR.add_object("star", *goal)


graph = Graph()
came_from, current = find_goal_bfs(start, goal, graph)
path = reconstruct_path(came_from, start, current)
for node in path:
    RUR.add_colored_tile("green", *node)

pause()
```

```py
from search_tools import (PriorityQueue,
                          manhattan_distance,
                          Graph,
                          reconstruct_path)
think(0)
RUR.set_world_size(14, 12)
frontier = PriorityQueue()
start = 3, 3, "east"
goal = 12, 10

recording(False)
for x in range(4, 11):
    RUR.add_background_tile("bricks", x, 11)
    RUR.add_background_tile("bricks", x, 2)
for y in range(3, 11):
    RUR.add_background_tile("bricks", 10, y)
recording(True)


RUR.add_object("token", start[0], start[1])
RUR.add_object("star", *goal)


frontier.add(start, 0)
graph = Graph(turn_left=True)
came_from = {}

came_from[start] = None


while not frontier.is_empty():
   current = frontier.get_best()

   if current[0] == goal[0] and current[1] == goal[1]:
      break

   for neighbour in graph.neighbours(current):
      if neighbour not in came_from:
         priority = manhattan_distance(goal, neighbour)
         frontier.add(neighbour, priority)
         came_from[neighbour] = current
   frontier.mark_done(current)

path = reconstruct_path(came_from, start, current)
for node in path:
    RUR.add_colored_tile("green", *node)

pause()
```