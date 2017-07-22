# Caution:

If you have stumbled upon this document, please be advised that many of the features described here are currently **not** available on the live version of [Reeborg's World](http://reeborg.ca/reeborg.html).

# A Teacher's Guide ...

This book is intended for those that create **worlds** \(i.e. programming tasks\) to help others learn programming using [Reeborg's World](http://reeborg.ca/reeborg.html).  In this book I will refer to you as a _**teacher**_ and to those that wish to learn programming using your creations as _**students**_.

Using the menu-driven world editor available in [Reeborg's World](http://reeborg.ca/reeborg.html), it is easy to create relatively simple worlds.  However, one can do much more using the advanced API. This book is a guide which should help you create more interesting  and challenging worlds for your students, while explaining other features of Reeborg's World.

## What I expect of you

I assume that you have a good working knowledge of writing programs using either Javascript or Python. I use mostly Python in the examples I give as I consider it to be easier to read than Javascript.

I also hope that you have already explored the user interface of Reeborg's World, doing more than simply writing and running programs. Ideally, you should already have created a few worlds using the menu-driven World editor, but that is not an absolutely necessary prerequisite to follow along as I give a step-by-step guide in the next chapter.

While I have included many screenshots to give examples, to get the full picture it is essential that you run examples on the site, especially when animations are involved: these simply cannot be given justice by simply showing a series of static images in a book like this one.

## About Reeborg's World

I am using the words _**Reeborg's World**_ to mean three different things. [Reeborg's World \(main site\)](http://reeborg.ca) is a website I designed to help people to learn programming. It includes a Python tutorial \(which is in constant need of updating\) available in English, French and Korean. However, **its main feature**, and the one referred to in this document, is a single-app page which is usually what I mean when I write [Reeborg's World](http://reeborg.ca/reeborg.html). Finally, I can refer to _Reerborg's world_ \(lower case _w_\) as a single programming task.

* **Reeborg's World is free;** you do not have to pay to use it.
  * I pay for the required hosting fees myself and currently have absolutely no plan to derive income from the site.
* Reeborg's World is open source; the main repository is public and can be found at [https://github.com/aroberge/reeborg](https://github.com/aroberge/reeborg).  I know that some teachers have installed a copy on their school servers for convenience and I have always try to offer support for those that want to do this.
  * **TODO:** add info about the special repository and update the information on that repository.
* Reeborg's World does not require users to log in.  In fact, there is no login feature.  Unless users \(teachers or students\) contact me, I have no way to know who you are.

  * I do use [Clicky ](https://clicky.com/)to keep track of how many people are using the site. However I know that some adblockers will disable Clicky.
  * I do not embed any social media widget, nor do I have any ads on the site. \[If the traffic on the site increases substantially, I might consider accepting support from a sponsor.\]
  * Reeborg's World does save the current state of a session in your browser's local storage, thus allowing to resume your work when you leave and come back to the site at a later time. I do not have access to this information.
  * There is a live collaboration feature available where two or more people can work together remotely; this makes use of Mozilla's server with [TogetherJS](https://togetherjs.com/). If you use this feature, Mozilla may know who you are - I do not.

* Reeborg's World is also designed with teachers in mind: while some basic **worlds **\(i.e. programming tasks\) are included by default, you can easily create and add your own. In fact, the motivation for writing this book was to give you the tools required to create interesting programming tasks.

### Learning programming

Reeborg's World is designed to help students learn programming in Python or Javascript. Reeborg's World is the natural evolution of a project which started in 2004 as a desktop program I wrote named RUR-PLE, and which is now obsolete. It is based on the [_Karel the robot_](http://www.amazon.ca/Karel-Robot-Gentle-Introduction-Programming/dp/0471089281/ref=sr_1_6?s=books&ie=UTF8&qid=1440177128&sr=1-6) approach introduced by Richard Pattis in 1981.

Reeborg's World has been created with the goal of keeping much of Pattis's basic idea, while still making it possible to introduce very advanced programming concepts.  So, instead of the "simple" **first program** found in some tutorials supposedly aimed  
at complete beginners:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
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

### Task Driven Learning

Reeborg's World is designed for _Task Driven Learning_: students are given tasks that Reeborg has to complete, and they must write programs instructing Reeborg how to do so. Feedback is given automatically to students, without requiring a teacher to be present.

Tasks include having Reeborg move objects, build walls, or go to a particular location.  Objects in Reeborg's World are colourful; the places they be must moved to by Reeborg are usually indicated by having a picture of the object in shades of grey.

![](/assets/simple_task.png)

While most programming tasks will likely be relatively simple and aimed at beginners, they is no limit to how complex a given programming task can be.  For example,  **very advanced students** can be given a maze with one or more objects to be collected and asked to

1. use the available methods to obtain a JSON description of the world;
2. transform this into some standard graph representation
3. use search techniques \(breadth-first or depth first\) to find the shortest path required to complete the task
4. accomplish the task following the path found, whose length can then be automatically compared with that of the true shortest path.[^2]

If you have some examples \(particularly tasks for Reeborg\) that you find useful for your students, I would appreciate if you could share them with me so as to improve Reeborg's World for everyone.

### A brief word about Blockly

In addition to writing programs using a code editor, Reeborg's World makes it possible to use visual programming blocks to write programs.

![](/assets/blockly_example.png)

This is made possible thanks to [Google's Blockly](https://developers.google.com/blockly/).

In their [Best practices document](https://developers.google.com/blockly/guides/app-integration/best-practices), the creators of Blockly mention the importance of having a so-called _exit strategy_.

> Block-based programming is often a starting point for programming. In the context of teaching computer programming, it is a gateway drug that gets students addicted, before moving them on to harder things. How long this block-based programming period should last for students is hotly debated, but if your goal is to teach programming it should be temporary.
>
> ...
>
> Block-based programming environments used for teaching programming need to have a concrete plan for graduating their students. A solid exit strategy also goes a long way towards placating those who argue that block-based programming isn't "real programming".

One feature of Reeborg's World is the possibility for the student to see how a program constructed using blocks would be translated into Python or Javascript, thus providing such an _exit strategy_.

![](/assets/blockly_example_python.png)

## Checklist for a good programming environment

In their 1997 paper, [Mini-languages: A Way to Learn Programming Principles](http://www.contrib.andrew.cmu.edu/~plb/papers/minilang.html)[^3], Brusilovsky _et.al._ provide an overview of the mini-language approach to teach programming and mention many requirements that they consider important for a successful application of a mini-language. Here I attempt to make a list of these requirements together with an explanation as to how Reeborg's World attempts to meet each requirement.

* _The mini-language should be **simple **in both its syntax and semantics._

  * Using the simple function based approach, with instructions like `move()` and `turn_left()`, and using Python as the basic programming language \(limiting to simple constructs\) meets this requirement - especially if one initially uses the fake Python keyword, `repeat n:` that I added to replace the standard construct `for variable in range(n):`; see the appendix on `repeat` for more details. 

* ... _most operations performed by the actor should make visible changes in the microworld represented on the screen._

  * This is the case with the robot world graphical representation.

* ... _any mini-language command can be executed in both navigation mode \(single command execution\) and programming mode \(complete program execution\)_.

  * With the Python REPL, single command executing is made possible; complete program execution is accomplished by using the code editors or the Blockly environment.

* _It should contain a mechanism for creating abstract instructions \(procedures\)._

  * This is done using Python's `def` or Javascript `function`. It is also supported by the Blockly interface.

* _The procedures designed for a particular problem can be later re-used for solving subsequent problems._

  * This is supported by providing a user's **library **when programming with Python.

* _The learning should be supported by a good programming environment. Such an environment should keep both the microworld and the student program visible on the screen._

  * This is how Reeborg's World has been designed to look from the very beginning - including its desktop predecessor, RUR-PLE.

* _The program should typically be executed one instruction at a time, while the interpreter highlights programming constructs in the source code as they are being executed and the effect is simultaneously shown in the microworld._

  * This is available by default when using Python as the programming language. One can step through the program one instruction at a time and even step backwards if needed.

* _The interpreter should also provide visualization for those concepts of the language that are not visualized by the microworld. Important features include visualization of variables and the stack of subroutine calls._

  * With the exception of the visualization of the stack of subroutine calls, this is possible with the somewhat experimental "watching variable" feature.

![](/assets/watch_vars1.png)

* _A good mini-language should be complemented with a good set of attractive and meaningful problems for students to solve._

  * I completely agree. Reeborg's World include a small set of such programming tasks \(worlds\) ... and I am counting on your to increase the number of such tasks available! :-\)

I do have one disagreement with the traditional mini-language approach: I believe that students can be more motivated to learn programming if they are using a "real" programming language rather than an artificial and limited one made up only to teach basic programming concepts.

### Support for non-English speaking students

Reeborg's World has been designed to support languages other than English. The User Interface currently supports English, French and Korean. The programming constructs are available in English and French.  This could "easily" be extended to other languages through user's contributions.

Some young students who are not used to writing using an ascii-based keyboard may find it difficult to write programs. To help them, Reeborg's World includes a special keyboard, which has three versions: one for traditional Python programming another for Javascript, and a third when using the Python REPL.

![](/assets/keyboard1.png)

![](/assets/keyboard2.png)

![](/assets/keyboard3.png)

![](/assets/keyboard4.png)

## A brief word about the organization of this book

In the early sections of this book, I have attempted to include absolutely all relevant details and required steps to understand the material introduced later. Admittedly, this makes for a rather slow going read if you follow along all the examples which is something I strongly recommend.

As the book progresses, the pace increases significantly. In some sections, I only give a cursory explanation of a topic and, most often, instead of including a complete code sample in the book, I ask you to load a specific world in Reeborg's World. This way, if I make changes to the code running the site, I only have to update the relevant worlds that I created without having to worry about correcting the code in this book.

If you do find that some explanations are missing or too brief to be of much use, please contact me with your suggestions so that I can improve the book.

The very last part of this book is a series of appendices. The most interesting of those is likely going to be the the list of worlds that include all relevant examples described in this book to which **My hope is that I will be able to add examples provided by people like you**!

[^1]: It is for this reason that I have added \`repeat\` as a fake Python keyword. See the appendix on \`repeat\` for more details.

[^2]: I have not created such a similar task; interested teachers are certainly welcome to contribute such advanced programming tasks.

[^3]: Brusilovsky, P., Calabrese, E., Hvorecky, J., Kouchnirenko, A., and Miller, P. \(1997\) Mini-languages: A Way to Learn Programming Principles. Education and Information Technologies 2 \(1\), pp. 65-83.

