# Search - just a draft to keep ideas

```js
var start, current, visited, frontier, i, neighbours, next;
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

Python version

```py
think(100)
RUR.set_world_size(5, 5)
frontier = Container()
visited = {}

start = (3, 3)
frontier.append(start)
visited[start] = True

while not frontier.is_empty():
    current = frontier.get_first()
    for neighbours in RUR.get_neighbours(current):
        next = tuple(neighbours)
        if next not in visited:
            frontier.append(next)
            visited[next] = next
    frontier.mark_done(current)  # changing color only

```



