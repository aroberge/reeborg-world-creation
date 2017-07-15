# Caution:

If you have stumbled upon this document, please be advised that many of the features described here are currently **not** available on the live version of [Reeborg's World](http://reeborg.ca/reeborg.html).

# About Advanced World Creation

This book is intended for those that create **worlds **\(i.e. programming tasks\) to help others learn programming using [Reeborg's World](http://reeborg.ca/reeborg.html).  In this book I will refer to you as a _teacher_ and to those that wish to learn programming as _students_.

Using the menu-driven world editor available in Reeborg's World, it is easy to create relatively simple worlds.  However, one can do much more using the advanced API. This book is a guide which should help you create more interesting worlds for your students.

### What I expect of you

I assume that you have a good working knowledge of writing programs using either Javascript or Python. I use mostly Python in the examples I give as I consider it to be easier to read than Javascript; I think it is also a better first language for students.

I also expect that you have explored the user interface of Reeborg's World, doing more than simply writing and running programs. Ideally, you should already have created a few worlds using the menu-driven World editor, but that is not necessary to follow along.

### About Reeborg's World

[Reeborg's World \(main site\)](http://reeborg.ca) is a website I designed to help people to learn programming. It includes a Python tutorial \(which is in constant need of updating\) available in English, French and Korean. However, its main feature, and the one referred to in this document, is a single-app page which I refer to simply as [Reeborg's World](http://reeborg.ca/reeborg.html).

* **Reeborg's World is free**.
  * I pay for the required hosting fees myself and currently have no plan to derive income from the site.  
* Reeborg's World is the natural evolution of a project which started in 2004 as a desktop program I wrote named RUR-PLE, and which is now obsolete. It is based on the _Karel the robot_ approach introduced by Richard Pattis in 1981.
* Reeborg's World does not require users to log in.  In fact, there is no login feature.  Unless users \(teachers or students\) contact me, I have no way to know who you are.  
  * I do use [Clicky ](https://clicky.com/)to keep track of how many people are using the site. However I know that some adblockers will disable Clicky. 
  * I do not embed any social media widget, nor have any ads on the site.
  * Reeborg's World does save the current state of a session in your browser's local storage, thus allowing to resume your work when you leave and come back to the site at a later time. I do not have access to this information.
  * There is a live collaboration feature available where two or more people can work together remotely; this makes use of Mozilla's server with [TogetherJS](https://togetherjs.com/). If you use this feature, Mozilla may know who you are - I do not.
* Reeborg's World is open source; the main repository can be found at [https://github.com/aroberge/reeborg](https://github.com/aroberge/reeborg).  I know that some teachers have installed a copy on their school servers.
* Reeborg's World is designed to help students learn programming in Python or Javascript, using either a traditional "code written in an editor" approach or a blockly interface; the blockly interface does not give access to the full programming possibilities from a student's point of view.
  * It supports a basic function-based approach \[e.g. `move()`\] as well as an OOP approach \[e.g. `reeborg.move()`\]. 
* Reeborg's World is also designed with teachers in mind: while some basic worlds are included by default, you can easily create and add your own. In fact, this is what this book is all about.





