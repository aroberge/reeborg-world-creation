# List, tuples, dicts

In all the examples below, I use the world **Alone** to ensure that there is a robot present at position \(1, 1\).



## List

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

## Tuples

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







