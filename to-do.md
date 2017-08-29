* add section with all images, and their source
* add section on suggested learning  plan for beginners, with motivation
* adapt the images from [https://opengameart.org/content/robot-0](https://opengameart.org/content/robot-0) to do a robot animation demo.

## Tests

> **\[info\] Some info**
>
> Some text

Other content

> **\[warning\] A warning**
>
> Some text

Other content

> **\[danger\] Dangerous**
>
> Some text

Other content

> **\[success\] Success!**
>
> Some text

* A\* algorithm [http://www.redblobgames.com/pathfinding/a-star/introduction.html](http://www.redblobgames.com/pathfinding/a-star/introduction.html) \(uses Queue\)
* Breadth-first search and Depth-first search [http://eddmann.com/posts/depth-first-search-and-breadth-first-search-in-python/](http://eddmann.com/posts/depth-first-search-and-breadth-first-search-in-python/) \(uses simpler data structures\)
  * [http://www.redblobgames.com/pathfinding/a-star/implementation.html](http://www.redblobgames.com/pathfinding/a-star/implementation.html) see Queue implementation
    * One solution is a hack, but it works some of the time. When iterating through neighbors, instead of always using the same ordering \(such as north, east, south, west\), change the ordering on “odd” grid nodes \(those where \(x+y\) % 2 == 1
* control animated gifs [https://stackoverflow.com/questions/39374962/control-gif-animation-with-js-play-stop-play-backwards](https://stackoverflow.com/questions/39374962/control-gif-animation-with-js-play-stop-play-backwards)

* For A\*, implement cost function related to number of turns: right turns are penalized more than left turns and, overall, the number of turns is minimized

  * alternative for straighter paths: treat left and right turns equally \(use RepairedRobot\) and penalize two consecutive moves compared with a turn \(or penalize weight based on manhattan heuristics?\)
  * this may require to reprioritize

* For graph demo, add tiles that are arrows \(see redblobames\); perhaps arrows with an offset to show the overlap, rather than staying into a normal grid square.

* add https://aroberge.blogspot.ca/2015/10/cryptic-reeborg.html
* 


