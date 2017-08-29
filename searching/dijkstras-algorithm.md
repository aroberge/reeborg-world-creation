# Dijkstra's algorithm

some explanation

```py
from search_tools import (PriorityQueue, 
                          manhattan_distance,
                          get_neighbours)
think(0)
RUR.get_current_world().small_tiles = True
RUR.set_world_size(14, 12)
frontier = PriorityQueue()
start = 3, 3
goal = 12, 10
RUR.add_object("token", *start)
RUR.add_object("star", *goal)

frontier.add(start, 0)
came_from = {}

came_from[start] = None

while not frontier.is_empty():
   current = frontier.get_lowest()

   if current == goal:
      break
   
   for next in get_neighbours(current):
      if next not in came_from:
         priority = manhattan_distance(goal, next)
         frontier.add(next, priority)
         came_from[next] = current
   frontier.mark_done(current)

pause()
```

Add screen capture; repeat search multiple times.



