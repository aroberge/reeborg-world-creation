# Protection against fatalities

Reeborg can "die" from interacting with `fatal` things such as:

* stepping on a fatal background tile;
* walking into a fatal obstacle;
* picking up a fatal object.

However, Reeborg can sometimes be protected against these fatal encounters:

* if a bridge, with the appropriate `protections`, is above an
  otherwise fatal background tile;
* if Reeborg carries an object with the appropriate protections.

To see how bridges can protect against fatal background tiles, but not  
obstacles, load up the following and click on **World Info** for the details  
prior to running the program:

```py
World("worlds/examples/protection_bridge.json")
```

Visually, this is hinted at by the fact that obstacles are drawn on top  
of bridges, and thus remain visible when a bridge is present \(and, in some  
case, the obstacles can hide the bridge altogether\).

To see how carried objects can protect against fatal background tiles, obstacles  
and picking up fatal objects, load up the following and click on **World Info** for the details  
prior to running the program:

```py
World("worlds/examples/protection_objects.json")
```

A more interesting example is

```py
World("worlds/examples/protection_example.json")
move()
take()
move()
move()
move()
put()
move()
move()
take()
move()
move()
move()
put()
move()
```

where we choose a different robot model automatically based on the protection given by the object carried.

![](/assets/protect1.png)![](/assets/protect2.png)![](/assets/protect3.png)

![](/assets/protect4.png)

![](/assets/protect5.png)

