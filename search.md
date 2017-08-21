# Search - just a draft to keep ideas

```js
var start, current, visited, frontier, i, neighbours, next;

RUR.set_world_size(5, 5)
start = [3, 3]
frontier = new Container()
frontier.append(start)
visited = {}
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
    frontier.set_done(current) // purely for aesthetics
}
```





