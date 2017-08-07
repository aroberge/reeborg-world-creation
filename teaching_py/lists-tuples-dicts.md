# Lists, tuples, and dicts

One of the goals I had in creating Reeborg's World was to have functions or methods that would return some basic data structures, such as Python's lists, tuples, and dict \(and their JavaScript equivalent, if possible\), thus giving a starting point to discuss such data structures in an environment that students were already familiar with.

In all the examples below, unless specified otherwise, I used the world **Alone** to ensure that there is a robot present at position \(1, 1\).

## List

> **\[info\] Why a list?**
>
> Using `object_here()`, Reeborg can see what kind of objects are present, but does not know how many of each are there. To find out the exact number, Reeborg would need to pick up the objects to count them.

```py
RUR.add_object("token", 1, 1, {'number': 4})
RUR.add_object("beeper", 1, 1, {'number': 7})
print(object_here())
print(object_here("token"))
print(object_here("apple"))
```

The result is:

```py
['token', 'beeper']
['token']
[]
```

The JavaScript equivalent to Python's lists are Arrays; running the following JavaScript program yields a result that looks identical to the above:

```js
RUR.add_object("token", 1, 1, {number: 4})
RUR.add_object("beeper", 1, 1, {number: 7})
write(object_here(), "\n")
write(object_here("token"), "\n")
write(object_here("apple"), "\n")
```

## Tuple

```py
print("Here:", position_here())
print("Facing East, in front:", position_in_front())

turn_left()
turn_left()

print("Here", position_here())
print("Facing West, in front:", position_in_front())
```

The result is:

```
Here: (1, 1)
Facing East, in front: (2, 1)
Here (1, 1)
Facing West, in front: ()
```

We can, of course, assign values

```py
# facing East at (1, 1)
x, y = position_in_front()
print("x =", x)
print("y =", y)
```

Which gives the following:

```
x = 2
y = 1
```

Note that Javascript does not have tuples; so arrays are returned instead.

```js
write("Here: ", position_here(), "\n")
write("In front: ", position_in_front(), "\n")
```

The result is:

```
Here: [1,1]
In front: [2,1]
```

## Dict

```py
RUR.give_object_to_robot("apple", 3)
RUR.give_object_to_robot("banana", 4)
print(carries_object())
```

The result is as follows:

```py
{'apple': 3, 'banana': 4}
```

For JavaScript, a simple object is returned:

```js
RUR.give_object_to_robot("apple", 3)
RUR.give_object_to_robot("banana", 4)
write(carries_object())
```

yields

```
{"apple":3,"banana":4}
```

Note however that if we specify an argument to `carries_object`, it is an integer \(the number of such objects being carried\) that is returned and not a dict \(nor an object in JavaScript\).

```py
RUR.give_object_to_robot("apple", 3)
RUR.give_object_to_robot("banana", 4)
print(carries_object("apple"))
print(carries_object("token"))
```

The result is:

```
3
0
```

**Caution: **if Reeborg carries no object, the returned value of `carries_object()` will be 0, and not an empty dict.

## For advanced students

A much more complex example of Python dict \(or JavaScript object\) is that of the "world map".  We start with a Python example:

```py
World("Tokens 1")
gps = SatelliteInfo()
gps.print_world_map()
```

The result looks something like the following:

```
{
  "robots": [
    {
      "x": 1,
      "y": 1,
      "prev_orientation": 0,
      "objects": {},
      "_orientation": 0,
      "_is_leaky": true,
      "_prev_x": 1,
  ...
```

with many more lines printed. For complex worlds, this can be **very** long.  We can access the information as a **dict** implemented as a Python property for the class.

```py
World("Tokens 1")
gps = SatelliteInfo()
goal = gps.world_map["goal"]
print(goal)
```

The printed result is not formatted as nicely as the previous "printed" version, but give us the required information.

```py
{'position': {'x': 4, 'y': 1}, 'objects': {'3,1': {'token': 1}}}
```

> **\[info\] French version**
>
> En français, une version équivalente du code décrit ci-dessus serait comme suit:
>
> ```py
> Monde("Jetons 1")
> gps = InfoSatellite()
> gps.imprime_carte()
> but = gps.carte_du_monde["goal"]
> print(but)
> ```

There is also a Javascript version which is available in both English and French as follows:

```js
var goal, map;
RUR.print_world_map();

map = RUR.world_map();
goal = map.goal;
write(goal)
```



