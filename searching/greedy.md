# Greedy algorithm

Add some explanation.

```py
from search_tools import (PriorityQueue,
                          manhattan_distance,
                          Graph)
think(0)
RUR.get_current_world().small_tiles = True
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
   current = frontier.get_lowest()

   if current == goal:
      break

   for next in graph.neighbours(current):
      if next not in came_from:
         priority = manhattan_distance(goal, next)
         frontier.add(next, priority)
         came_from[next] = current
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
   current = frontier.get_lowest()

   if current == goal:
      break

   for next in graph.neighbours(current):
      if next not in came_from:
         priority = manhattan_distance(goal, next)
         frontier.add(next, priority)
         came_from[next] = current
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