# Caution:

If you have stumbled upon this document, please be advised that many of the features described here are currently **not** available on the live version of [Reeborg's World](http://reeborg.ca/reeborg.html).

# About Advanced World Creation

This very short book is intended for those that create **worlds** \(i.e. programming tasks\) to help others learn programming using [Reeborg's World](http://reeborg.ca/reeborg.html).  In this book I will refer to you as a _**teacher**_ and to those that wish to learn programming using your creations as _**students**_.

Using the menu-driven world editor available in Reeborg's World, it is easy to create relatively simple worlds.  However, one can do much more using the advanced API. This book is a guide which should help you create more interesting  and challenging worlds for your students, while explaining other features of Reeborg's World.

### What I expect of you

I assume that you have a good working knowledge of writing programs using either Javascript or Python. I use mostly Python in the examples I give as I consider it to be easier to read than Javascript.

I also hope that you have already explored the user interface of Reeborg's World, doing more than simply writing and running programs. Ideally, you should already have created a few worlds using the menu-driven World editor, but that is not necessary to follow along as I give a step-by-step guide in the next chapter.

While I have included many screenshots to give examples, to get the full picture it is essential that you run examples on the site, especially when animations are involved: these simply cannot be given justice by simply showing a series of static images in a book like this one.

### About Reeborg's World

[Reeborg's World \(main site\)](http://reeborg.ca) is a website I designed to help people to learn programming. It includes a Python tutorial \(which is in constant need of updating\) available in English, French and Korean. However, **its main feature**, and the one referred to in this document, is a single-app page which I refer to simply as [Reeborg's World](http://reeborg.ca/reeborg.html).

* **Reeborg's World is free;** you do not have to pay to use it.
  * I pay for the required hosting fees myself and currently have absolutely no plan to derive income from the site.
* Reeborg's World is open source; the main repository is public and can be found at [https://github.com/aroberge/reeborg](https://github.com/aroberge/reeborg).  I know that some teachers have installed a copy on their school servers for convenience and I have always try to offer support for those that want to do this.
* Reeborg's World does not require users to log in.  In fact, there is no login feature.  Unless users \(teachers or students\) contact me, I have no way to know who you are.

  * I do use [Clicky ](https://clicky.com/)to keep track of how many people are using the site. However I know that some adblockers will disable Clicky.
  * I do not embed any social media widget, nor do I have any ads on the site. \[If the traffic on the site increases substantially, I might consider accepting support from a sponsor.\]
  * Reeborg's World does save the current state of a session in your browser's local storage, thus allowing to resume your work when you leave and come back to the site at a later time. I do not have access to this information.
  * There is a live collaboration feature available where two or more people can work together remotely; this makes use of Mozilla's server with [TogetherJS](https://togetherjs.com/). If you use this feature, Mozilla may know who you are - I do not.

* Reeborg's World is designed to help students learn programming in Python or Javascript, using either a traditional "code written in an editor" approach or a blockly interface; the blockly interface does not give access to the full programming possibilities from a student's point of view.

  * It supports a basic function-based approach \[e.g. `move()`\] as well as an OOP approach \[e.g. `reeborg.move()`\].
  * Reeborg's World is the natural evolution of a project which started in 2004 as a desktop program I wrote named RUR-PLE, and which is now obsolete. It is based on the _Karel the robot_ approach introduced by Richard Pattis in 1981.

* Reeborg's World is also designed with teachers in mind: while some basic **worlds **\(i.e. programming tasks\) are included by default, you can easily create and add your own. In fact, this is what this book is all about.

## About this book

I have broken down various topics into "chapters", each of which barely deserves the name as they are so short.

In the early chapters of this book, I have attempted to include absolutely all relevant details and required steps to understand the later chapters. Admittedly, this makes for a rather slow going read if you follow along all the examples which is something I strongly recommend.

As the book progresses, the pace increases significantly. In some chapters, I only give a cursory explanation of a topic and, most often, instead of including a complete code sample in the book, I ask you to load a specific world in Reeborg's World. This way, if I make changes to the code running the site, I only have to update the relevant worlds that I created without having to worry about correcting the code in this book.

Finally, there are a series of appendices. The most interesting of those is likely going to be the the list of worlds that include all relevant examples described in this book to which **I plan to add examples provided by people like you**!

