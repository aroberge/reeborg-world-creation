For simple path, show that

```py
while not at_goal():
    x, y = position_in_front()
    if RUR.is_background_tile("gravel", x, y):
        move()
        if x==6 and y==1:
            move()
            turn_left()
            turn_left()
            move()
            turn_left()
            turn_left()
    else:
        turn_left()
```

only gives a message at the very end indicating that the path was not followed. Using the decorator pattern, it is possible to give information as soon as the path is no longer followed.



