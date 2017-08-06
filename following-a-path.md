# Following a path

In this section, I consider a very simple example which requires the student to have Reeborg following a predefined path to reach its home. The end goal is to come up with code \(in the Pre and Post editors\) which can verify that the correct solution has been found.

 ![](/assets/easy_path.png)

No obstacle exists in this world, so, a-priori, Reeborg could take any path and achieve the goal. However, we want Reeborg to not walk on the grass and take the minimum amount of instructions possible; here's a simple solution in Python:

```py
World("worlds/examples/easy_path.json") # I will no longer include this line below
move()
move()
turn_left()
move()
```

And here's a completely equivalent solution:

```py
while front_is_clear():
    move()
turn_left()
move()
```

This type of problem could be equally suitable for beginners, with a simple world like this one, or for very advanced students who have to find the shortest path to accomplish a given task in a maze-like world generated randomly each time it is run.

## Finding the solution

The first step is to find the correct solution.  In this particular case, it is trivial:





