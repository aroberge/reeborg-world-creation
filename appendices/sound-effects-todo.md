# Sound effects

Some sound effects are available; they can be turned on and off at any point in a program using `sound(True)` or `sound(False)`. At present, I consider this to be more of a proof-of-concept feature, although I am told that it is popular with some young children.

I have found that sound effects are not always played reliably when too little time is available for each action; thus, except for the sound effect at the very end of the program's execution, sound effects are turned off if the delay between each frame being displayed, set using the `think(delay)` function, is less than 250 ms, even if the user included a `sound(True)` command.

At some point in the future, I will likely revisit the way I've implemented sound effects in an attempt to make them more interesting ... and find a way to include sound effects for beepers: I will likely have sound from beepers being turned on only when Reeborg would be at a grid location where beepers are present, as it is described in the original Karel the robot.

