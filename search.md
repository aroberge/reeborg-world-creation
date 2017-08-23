# Search - just a draft to keep idea

See [http://www.redblobgames.com/pathfinding/a-star/introduction.html](http://www.redblobgames.com/pathfinding/a-star/introduction.html) for details. Add explanations about the site, and refer readers to complementary views whenever appropriate.



To be added:

* explain how one can change the default colors
* add images

```py
from search_tools import Container, get_neighbours
World("empty")
think(100)

RUR.set_world_size(5, 5)
frontier = Container()
visited = {}

start = (3, 3)
frontier.append(start)
visited[start] = True

while not frontier.is_empty():
    current = frontier.get_first()
    for neighbour in get_neighbours(current):
        if neighbour not in visited:
            frontier.append(neighbour)
            visited[neighbour] = True
    frontier.mark_done(current)  # changing color only
```

Add goal \(turn off highlighting\)

```py
from search_tools import Container, get_neighbours
World("empty")
think(100)
no_highlight()

RUR.set_world_size(10, 10)
frontier = Container()
visited = {}

start = (3, 3)
goal = (6, 4)
RUR.add_object("star", *goal)
frontier.append(start)
visited[start] = True

while not frontier.is_empty():
    current = frontier.get_first()
    for neighbour in get_neighbours(current):
        if neighbour not in visited:
            frontier.append(neighbour)
            visited[neighbour] = True
            if neighbour == goal:
                done()
    frontier.mark_done(current)  # changing color only
```

Put in function

```py
from search_tools import Container, get_neighbours
World("empty")
think(100)
no_highlight()

RUR.set_world_size(10, 10)
frontier = Container()
visited = {}

start = (3, 3)
goal = (6, 4)
RUR.add_object("star", *goal)
frontier.append(start)
visited[start] = True

def find_goal():
    while not frontier.is_empty():
        current = frontier.get_first()
        for neighbour in get_neighbours(current):
            if neighbour not in visited:
                frontier.append(neighbour)
                visited[neighbour] = True
                if neighbour == goal:
                    return
        frontier.mark_done(current)  # changing color only

find_goal()
```

Get path

```py
from search_tools import Container, get_neighbours
World("empty")
think(100)
no_highlight()

RUR.set_world_size(10, 10)
frontier = Container(no_colors=True)
came_from = {}

start = (3, 3)
goal = (6, 4)
RUR.add_object("star", *goal)
RUR.add_object("token", *start)
frontier.append(start)
came_from[start] = None

def find_goal():
    while not frontier.is_empty():
        current = frontier.get_first()
        for neighbour in get_neighbours(current):
            if neighbour not in came_from:
                frontier.append(neighbour)
                came_from[neighbour] = current
                if neighbour == goal:
                    return
        frontier.mark_done(current)  # changing color only

find_goal()

current = goal 
path = [current]
while current != start: 
    current = came_from[current]
    path.append(current)

path.reverse()

for cell in path:
    RUR.add_colored_tile("maroon", *cell)
```

Add robot, remove think\(100\), do not append start,etc.

```py
from search_tools import Container, get_neighbours
World("empty")
no_highlight()

RUR.set_world_size(10, 10)
frontier = Container(no_colors=True)
came_from = {}

start = (3, 3)
goal = (6, 4)
RUR.add_final_position("house", *goal)
reeborg = UsedRobot(*start)
frontier.append(start)
came_from[start] = None

def find_goal():
    while not frontier.is_empty():
        current = frontier.get_first()
        for neighbour in get_neighbours(current):
            if neighbour not in came_from:
                frontier.append(neighbour)
                came_from[neighbour] = current
                if neighbour == goal:
                    return
        frontier.mark_done(current)  # changing color only

find_goal()

current = goal 
path= []
while current != start: 
    path.append(current)
    current = came_from[current]

path.reverse()

for cell in path:
    while cell != reeborg.position_in_front():
        reeborg.turn_left()
    reeborg.move()
```

## JavaScript versions

```js
var start, current, visited, frontier, i, neighbours, next;
World("empty")
think(100);
RUR.set_world_size(5, 5)
frontier = new RUR.Container()
visited = {}

start = [3, 3]
frontier.append(start)
visited[start] = true

while (!frontier.is_empty()){
    current = frontier.get_first();
    neighbours = RUR.get_neighbours(current);
    for(i=0; i<neighbours.length; i++) {
        next = neighbours[i];
        if (Object.keys(visited).indexOf(next) == -1) {
            frontier.append(next)
            visited[next] = next
        }
    }
    frontier.mark_done(current); // changing color only
}
```



