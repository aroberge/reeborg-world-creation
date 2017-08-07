# Beepers

> **\[success\] New and improved**
>
> Beepers are back in Reeborg's World!

To understand what is meant by this statement, a bit of history is required. This chapter includes very little material that can be used to help you understand how to create interesting worlds. However, it may help you understand the reasoning behind some choices I made, and perhaps prompt you to make suggestions for other improvements.  In addition, it will illustrate a useful feature for students and introduce you to the basics of creating animated objects in Reeborg's World.

## The original Karel

When Pattis created Karel, it included beepers as objects that Karel could interact with.  As described in the book [Karel the robot](https://www.amazon.ca/Karel-Robot-Gentle-Introduction-Programming/dp/0471089281/ref=sr_1_12?s=books&ie=UTF8&qid=1500888110&sr=1-12), Karel could handle beepers via two instructions:

```
pickbeeper
putbeeper
```

Karel could detect if beepers were present using these two conditions:

```
next-to-a-beeper
not-next-to-a-beeper
```

Similarly, Karel could detect if it was carrying beepers \(in its bag\):

```
any-beepers-in-bag
no-beepers-in-bag
```

## Karel's children

From what I have read, I understand that Pattis did not create an actual simulator to run Karel's program. However, his idea proved so popular that many people adapted his idea and created simulators.  Most followed his exact design, except that they adapted the instructions names to follow the conventions of their own languages, most often using camelCase names, as in:

```
pickBeeper
anyBeeperInBag
```

A typical world would be represented as follows[^1]:

![](/assets/staircase.gif)                     ![](/assets/GreenfootKarel.png)

## RUR-PLE's beepers

I created RUR-PLE in 2004 as a means to teach myself Python. Like many others, I decided to follow my programming language's convention to write the various functions.  Python programmers traditionally use underscores to separate individual words making up a programming instruction instead of camelCase names. I also made some slightly different choices for some names and made use of the existence of the logical `not` keyword; here are a few instructions

```py
pick_beeper()
put_beeper()
carries_beepers()        # instead of any_beepers_in_bag()
not carries_beepers()    # instead of no_beepers_in_bag()
next_to_a_beeper()       # original name
on_beeper()              # name change after receiving commments
```

Like most others before, I represented beepers as circles; however, I also added the number of beepers present:

![](/assets/harvest-rurple.png)

From some feedback I received and from my own experience teaching Physics, I thought that this could perhaps be improved upon by replacing beepers.

## The problematic beepers

In the early feedback I received from RUR-PLE's users, one comment that struck me is that the name for the condition `next_to_a_beeper()` condition was confusing some students who thought that this meant that Reeborg had to be on a square adjacent to a beeper to detect it.  This lead me to change the name to `on_beeper()` while keeping the older name available to avoid creating problems for teachers and students using the older name. Still I saw some problems.  Here's how one author introduces beepers in Karel's world[^2].

> **beepers**
>
> Within Karel's world may be zero or more **beepers. **Beepers are small objects that emit a quiet beeping noise that Karel can "hear". When present, they are located at intersections \(like Karel\), which means when Karel is at a particular intersection, he might be "next to" a beeper, if there is one located where he is located. Karel can pick beepers up and put them into his "beeper bag" \(see below\) or take them out of his beeper bag and put them down at the intersection at which he is located. More than one beeper may be located at any given intersection.
>
> **Karel's beeper bag**
>
> Karel has a beeper bag into which he can put any number of beepers. The bag is made of a material that completely blocks the sound emitted by the beepers. This means that Karel will never "accidentally" "hear" a beeper in his bag. If he hears a beeper while at an intersection it is because there is a beeper at that intersection that is not in his bag.

As someone who taught introductory Physics for many years, this reminds me of a typical "frictionless, massless, ..." problem statement:

> Two objects are connected by an unstretchable massless string passing over a massless frictionless pulley. Ignoring air resistance, and assuming that the acceleration due to gravity does not depend on the height, calculate ...

The reason why we introduce so many qualifiers \(massless, frictionless, unstrechable, ...\) when teaching Physics is because the students would not be able to do the calculation taking into account these real effects with which they are familiar from the world they live in.

Reeborg/Karel's world is not something that students live in. It should be possible to design such imaginary worlds without having to worry about needing to redefine familiar expressions such as "next to" or having to describe fictitious material such as that with which the bag is made and which completely blocks the sound emitted by the beepers.  The circles in Karel's world do not look like beepers; they could be anything. I do understand the idea that Karel might need to be very close to a beeper to hear it, whereas he could see it from further away: thus the restriction in the use of the condition `nextToABeeper`.

Finally, computers are quite capable of making sounds. Having objects that are described as producing sound but such that the students could not hear them is not ideal. In fact, this was the number one suggestion/request for improvement I received for RUR-PLE.

## The initially beeperless Reeborg's World

When I created Reeborg's World, I originally replaced beepers by "tokens". To detect tokens, Reeborg initially used `token_here()` instead of something like `next_to_a_token()`. Soon, I added other objects and this was replaced by `object_here()`. More objects meant being able to create more visually interesting worlds. Having multiple objects also gave the added bonus of being able to have an easy and natural way to introduce \[optional\] function arguments, such as `object_here("token")`: thus, one more concept could be taught in an environment with which students had become familiar.

Still, I did occasionally get some requests to add beepers, from teachers familiar with either Karel or RUR-PLE.

## Beepers in Reeborg's World

Reeborg's World now includes beepers as one possible object type. Visually, they are represented by a series of images

![](/assets/beeper0.png) ![](/assets/beeper1.png) ![](/assets/beeper2.png) ![](/assets/beeper3.png)

which cycle repeately resulting in this amination: ![](/assets/beeper.gif)

If you hover your mouse over the image of Reeborg in a given world, you can see how many objects of each type it is carrying:

![](/assets/reeborg_carries.png)

When carried by Reeborg, beepers are "clearly" silent. Still, one would have to explain why...

Reeborg's world has the possibility to include sounds \(see the relevant appendix\).  However, it does not always work well and is something that I intend to improve.  You can turn sound on at any part of a program by including `sound(True)`. Currently, there is no sound effect to indicate that beepers are present.

[^1]: Source of the images: [https://www.cs.mtsu.edu/~untch/karel/fundamentals.html](https://www.cs.mtsu.edu/~untch/karel/fundamentals.html) and [https://csis.pace.edu/~bergin/KarelJava2ed/greenfoot.html](https://csis.pace.edu/~bergin/KarelJava2ed/greenfoot.html).

[^2]: Adapted \(with a very minor change\) from [http://karelsim.com/reference\_overview.html](http://karelsim.com/reference_overview.html)

