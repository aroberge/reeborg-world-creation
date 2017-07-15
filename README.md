# Caution:

If you have stumbled upon this document, please be advised that many of the features described here are currently **not** available on the live version of [Reeborg's World](http://reeborg.ca/reeborg.html).

# About Advanced World Creation

This book is intended for those that create **worlds **\(i.e. programming tasks\) to help others learn programming using [Reeborg's World](http://reeborg.ca/reeborg.html).  In this book I will refer to you as a _teacher_ and to those that wish to learn programming as _students_.

Using the menu-driven world editor available in Reeborg's World, it is easy to create relatively simple worlds.  However, one can do much more using the advanced API. This book is a guide which should help you create more interesting worlds for your students.

### What I expect of you

I assume that you have a good working knowledge of writing programs using either Javascript or Python. I use mostly Python in the examples I give as I consider it to be easier to read than Javascript; I think it is also a better first language for students.

### About Reeborg's World

[Reeborg's World \(main site\)](http://reeborg.ca) is a website I designed to help people to learn programming. It includes a Python tutorial \(which is in constant need of updating\) available in English, French and Korean. However, its main feature, and the one referred to in this document, is a single-app page which I refer to simply as [Reeborg's World](http://reeborg.ca/reeborg.html).

* **It is free**.
  * I pay for the required hosting fees myself and currently have no plan to derive income from the site.  It is the natural evolution of a project which started in 2004 as a desktop program named RUR-PLE \(now obsolete\).
* It does not require users to log in.  In fact, there is no login feature.  Unless users \(teachers or students\) contact me, I have no way to know who you are.  
  * I do use [Clicky ](https://clicky.com/)to keep track of how many people are using the site. However I know that some adblockers will disable Clicky. 
  * I do not embed any social media widget, nor have any ads on the site.
  * Reeborg's World does save the current state of a session in your browser's local storage, thus allowing to resume your work when you leave and come back to the site at a later time. I do not have access to this information.
  * There is a live collaboration feature available where two or more people can work together remotely; this makes use of Mozilla's server with [TogetherJS](https://togetherjs.com/). If you use this feature, Mozilla may know who you are - I do not.
* It is open source; the main repository can be found at [https://github.com/aroberge/reeborg](https://github.com/aroberge/reeborg).  I know that some teachers have installed a copy on their school servers.
* It is designed to help students learn programming in Python or Javascript, using either a traditional "code written in an editor" approach or a blockly interface; the blockly interface does not give access to the full programming possibilities from a student's point of view.
  * It supports a basic function-based approach \[e.g. `move()`\] as well as an OOP approach \[e.g. `reeborg.move()`\]. 
* It is also designed with teachers in mind: while some basic worlds are included by default, you can easily create and add your own. In fact, this is what this book is all about.

Reeborg's World is based on the _Karel the robot_ approach introduced by Richard Pattis in 1981.

### Karel vs Reeborg

Here's an image taken from a relatively recent version of Karel the Robot that is used to teach Java. \(See [https://csis.pace.edu/~bergin/KarelJava2ed/Karel++JavaEdition.html](https://csis.pace.edu/~bergin/KarelJava2ed/Karel++JavaEdition.html)\)

![](/assets/kjr2.gif)

Karel's world can have walls, blocking the way, and beepers, which are artefact which can be picked up and put down by Karel. To my knowledge, a given version of Karel can only be programmed using an OOP approach or a simple function based approach \(like Pattis's original version\).

By contrast, worlds in Reeborg's World can have multiple artefacts with which Reeborg can interact, including animated images.

![](/assets/nice_path.png)

If a programming task has defined goals, a student can receive feedback automatically after their program has executed indicating whether the expected task has been completed or not.

![](/assets/bad_result.png)

![](/assets/good_result.png)

There are many more features available in Reeborg's World, too many to describe here without the appropriate context. This book's aim is to document everything that is possible to do with Reeborg's World.

