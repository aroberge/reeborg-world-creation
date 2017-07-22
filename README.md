# Caution:

If you have stumbled upon this document, please be advised that many of the features described here are currently **not** available on the live version of [Reeborg's World](http://reeborg.ca/reeborg.html).

# A Teacher's Guide ...

This book is intended for those that create **worlds** \(i.e. programming tasks\) to help others learn programming using [Reeborg's World](http://reeborg.ca/reeborg.html).  In this book I will refer to you as a _**teacher**_ and to those that wish to learn programming using your creations as _**students**_.

Using the menu-driven world editor available in Reeborg's World, it is easy to create relatively simple worlds.  However, one can do much more using the advanced API. This book is a guide which should help you create more interesting  and challenging worlds for your students, while explaining other features of Reeborg's World.

## What I expect of you

I assume that you have a good working knowledge of writing programs using either Javascript or Python. I use mostly Python in the examples I give as I consider it to be easier to read than Javascript.

I also hope that you have already explored the user interface of Reeborg's World, doing more than simply writing and running programs. Ideally, you should already have created a few worlds using the menu-driven World editor, but that is not an absolutely necessary prerequesite to follow along as I give a step-by-step guide in the next chapter.

While I have included many screenshots to give examples, to get the full picture it is essential that you run examples on the site, especially when animations are involved: these simply cannot be given justice by simply showing a series of static images in a book like this one.

## About Reeborg's World

I am using the words _**Reeborg's World**_ to mean three different things. [Reeborg's World \(main site\)](http://reeborg.ca) is a website I designed to help people to learn programming. It includes a Python tutorial \(which is in constant need of updating\) available in English, French and Korean. However, **its main feature**, and the one referred to in this document, is a single-app page which I refer to simply as [Reeborg's World](http://reeborg.ca/reeborg.html). Finally, I can refer to _Reerborg's world_ (lower case _w_) as a single programming task.

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

Reeborg's World is designed to help students learn programming in Python or Javascript. Reeborg's World is the natural evolution of a project which started in 2004 as a desktop program I wrote named RUR-PLE, and which is now obsolete. It is based on the _Karel the robot_ approach introduced by Richard Pattis in 1981.

http://www.amazon.ca/Karel-Robot-Gentle-Introduction-Programming/dp/0471089281/ref=sr_1_6?s=books&ie=UTF8&qid=1440177128&sr=1-6


Reeborg's World has been created with the goal of keeping much of Pattis's
idea as much as possible, while still making it possible to
introduce very advanced programming concepts.  So, instead of the
"simple" **first program** found in some tutorials supposedly aimed
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

However, one is not limited to simple functions.
For example, if one wants to use an OOP approach instead,
the simplest valid Python program, which has Reeborg actually do the
equivalent to the single move()` instruction above, is:

```
reeborg = UsedRobot()
reeborg.move()
```
Similarly, because using standard libraries is something useful, students
can first learn about libraries by writing their own code and, in doing so,
they learn that library modules are just programs like any others.
Assuming they have defined a function, say turn_right()`, in their library,
the following program will be valid:

```py
from library import turn_right
turn_right()
```

So, the idea is to have the student deal with as few concepts as possible
to write programs, only learning new concepts (such as using variables,
or Object-Oriented notation, or importing code from a library)
after they have learned the basics.

However, the simplicity of the approach used in Reeborg's World
does not mean that what can be done is limited to the basics of the
virtual robot world.
The Python version of Reeborg's World is based on Brython, and includes
many Python modules found in Python's standard library which can be used
to write advanced programs.

### Task Driven Learning

Reeborg's World is designed for _Task Driven Learning_: students are given
tasks that Reeborg has to complete, and they must write programs instructing
Reeborg how to do so.

Tasks include having Reeborg move objects, build walls, or go to a
particular location.  Objects in Reeborg's World are colourful; the
places they be must moved to by Reeborg are indicated by having a
picture of the object in shades of grey.

While most programming tasks will likely be relatively simple and aimed at beginners, very advanced student can be given a complicated world (let's call it a _maze_) and asked to

  1. use the available methods to obtain a JSON description of the world;
  2. transform this into some standard graph representation
  3. use search techniques (breadth-first or depth first) to find the shortest path required to complete the task
  4. accomplish the task following the shortest path found, which can be automatically compared with the path.

If you have some examples (particularly tasks for Reeborg)
that you find useful for your students, I would appreciate
if you could share them with me so as to improve Reeborg's World for everyone.

## Checklist for a good programming environment

Details here.

## A brief word about the organization of this book

In the early sections of this book, I have attempted to include absolutely all relevant details and required steps to understand the material introduced later. Admittedly, this makes for a rather slow going read if you follow along all the examples which is something I strongly recommend.

As the book progresses, the pace increases significantly. In some sections, I only give a cursory explanation of a topic and, most often, instead of including a complete code sample in the book, I ask you to load a specific world in Reeborg's World. This way, if I make changes to the code running the site, I only have to update the relevant worlds that I created without having to worry about correcting the code in this book.

If you do find that some explanations are missing or too brief to be of much use, please contact me with your suggestions so that I can improve the book.

The very last part of this book is a series of appendices. The most interesting of those is likely going to be the the list of worlds that include all relevant examples described in this book to which **My hope is that I will be able to add examples provided by people like you**!

