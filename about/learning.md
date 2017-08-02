## Learning programming

Reeborg's World is designed to help students learn programming in Python or Javascript. Reeborg's World is the natural evolution of a project which started in 2004 as a desktop program I wrote named RUR-PLE, and which is now obsolete. It is based on the [_Karel the robot_](http://www.amazon.ca/Karel-Robot-Gentle-Introduction-Programming/dp/0471089281/ref=sr_1_6?s=books&ie=UTF8&qid=1440177128&sr=1-6) approach introduced by Richard Pattis in 1981.

Reeborg's World has been created with the goal of keeping much of Pattis's basic idea, while still making it possible to introduce very advanced programming concepts.  So, instead of the "simple" **first program** found in some non Karel-based tutorials supposedly aimed at complete beginners:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
    }
}
```

or the equivalent Karel program from a well-known version:

```java
import stanford.karel.*;
public class KarelMove extends Karel {
    public void run(){
        move();
    }
}
```

the simplest valid program in Reeborg's World is:

```
move()
```

That's it: a single instruction.  What could be simpler when teaching beginners?

However, one is not limited to simple functions. For example, if one wants to use an OOP approach instead, the simplest valid Python program, which has Reeborg actually do the equivalent to the single `move()` instruction above, is:

```
reeborg = UsedRobot()
reeborg.move()
```

Similarly, because using standard libraries is something useful, students can first learn about libraries by writing their own code and, in doing so, they learn that library modules are just programs like any others. Assuming they have defined a function, say `turn_right()`, in their library, the following program will be valid:

```py
from library import turn_right
turn_right()
```

So, the idea is to have the student deal with as few concepts as possible to write programs[^1], only learning new concepts \(such as using variables, or Object-Oriented notation, or importing code from a library\) after they have learned the basics.

However, the simplicity of the approach used in Reeborg's World does not mean that what can be done is limited to the basics of the virtual robot world. The Python version of Reeborg's World is based on [Brython](http://brython.info/), and includes many Python modules found in Python's standard library which can be used to write advanced programs.

[^1]: It is for a reason similar to this that I have added `repeat` as a fake Python keyword. See the section on `repeat` for more details.

