# Introduction

> **\[warning\] Warning**
>
> This book documents the new version of [Reeborg's World](http://reeborg.ca/reeborg.html), which has just been released and has not been fully tested by outside users.
>
> This book has not been completed yet.

This book, _**Reeborg's World: a Teacher's Guide**_, is intended for those who create **worlds** \(i.e. programming tasks\) to help others learn programming using [Reeborg's World](http://reeborg.ca/reeborg.html).  In this book I will refer to you as a _**teacher**_ and to those who wish to learn programming using your creations as _**students**_.

Using the menu-driven world editor available in [Reeborg's World](http://reeborg.ca/reeborg.html), it is easy to create relatively simple worlds.  However, one can do much more using the advanced API. This book is a guide which should help you create more interesting  and challenging worlds for your students, while explaining other features of Reeborg's World.

## What I expect of you

I assume that you have a good working knowledge of writing programs using either Javascript or Python. I use mostly Python in the examples I give as I consider it to be easier to read than Javascript. If you are helping someone else learn programming using either Python or Javascript, and need some help beyond what I offer in this book, please do not hesitate to contact me.

I also hope that you have already explored the user interface of Reeborg's World, doing more than simply writing and running programs. Ideally, you should already have created a few worlds using the menu-driven World editor, but that is not an absolutely necessary prerequisite to follow along as I give a step-by-step guide in the next chapter.

While I have included many screenshots to give examples, to get the full picture it is essential that you run examples on the site, especially when animations are involved: these simply cannot be given justice by simply showing a series of static images in a book like this one.

> **\[info\] Work in progress**
>
> I now consider that the web version of the book is more important than any other version \(like a pdf\). Since animated images are usable online, I have started to include animated images and plan to continue doing so.

## A brief word about the organization of this book

In the early sections of this book, I have attempted to include absolutely all relevant details and required steps to understand the material introduced later. Admittedly, this makes for a rather slow going read if you follow along all the examples which is something I strongly recommend.

As the book progresses, the pace increases significantly. In some sections, I only give a cursory explanation of a topic and, most often, instead of including a complete code sample in the book, I ask you to load a specific world in Reeborg's World. This way, if I make changes to the code running the site, I only have to update the relevant worlds that I created without having to worry about correcting the code in this book.

If you do find that some explanations are missing or too brief to be of much use, [please submit a request](https://github.com/aroberge/reeborg/issues).

The very last part of this book is a series of appendices. The most interesting of those is likely going to be the list of worlds that includes all relevant examples described in this book. **My hope is that I will be able to add examples provided by people like you**!

## A brief word about me

I am a physicist by training who has picked up programming as a hobby when my children were in elementary school, more than 10 years ago. I have no formal education in computer science and am continuously learning as I pursue my hobby. Other than the learning tasks mentioned in this book, the programs I wrote, including the code running Reeborg's site itself, should not be viewed as good examples to learn from. However, I do hope that with my perpetual beginner's hat on, I have created a site that makes learning programming accessible to beginners.

## Acknowledgements

This book is one more step in a journey that began in 2004, when I set about to learn Python and created RUR-PLE, as a desktop program. Many people helped me learn Python and create RUR-PLE and Reeborg's World; I couldn't possibly remember them all[^1] but a few offered some crucial comments, criticisms and suggestions, and I would be remiss if I did not mention them.

During the early days of learning Python and creating RUR-PLE, I received a lot of help from Peter Damoc, Waseem Daher and especially Stas Zytkiewicz. Early in the project, my life partner, T.P., suggested that I should change the name of the robot from its first name, Egrebor, to Reeborg: this is a **much** better name for the little robot. Over the years, T.P. has quite often volunteered to proofread my writings without ever showing signs of impatience at my oft-repeated written mistakes.

Andy Judkis, and his students, who were amongst the first dedicated users of RUR-PLE, offered many suggestions which lead to many, many improvements. Their enthusiasm helped to sustain mine during the early years of this project.

It was from a suggestion of Steve Howell for the Guido van Robot project that I decided to do the same for mine and move RUR-PLE to the web, thus creating Reeborg's World. Steve mentioned this idea in 2008 and even created a primitive version called Webster van Robot.  After many false starts, in early 2014, I finally created a web version good enough to be announced on my blog: [Reeborg's World was officially born.](https://aroberge.blogspot.ca/2014/03/reeborg-news.html)

[Andres Castano ](http://codeperspectives.com/) and his students were early users of Reeborg's World. Andres made many suggestions for improvements and was incredibly patient when changes I made to the site were breaking his code examples. Andres also contributed three different image types for the robot still in use today. Jurgis Pralgauskis also made many suggestions for improvements; in particular, he created a prototype of what became **Reeborg's Keyboard** and offered some suggestions \(and prodding\) which made it possible for me to implement the **watch variables** feature of Reeborg's World. Vincent Maille, lead author of [Les robots](https://www.amazon.ca/Robots-Apprendre-Robotique-Par-lExemple/dp/2340013984/ref=sr_1_1?ie=UTF8&qid=1500382251&sr=8-1&keywords=les+robots+maille), also made many suggestions for improvements and contributed some bug reports. About a third of the book _**Les robots**_ describes how to use Reeborg's World to learn programming.

Python's support for Reeborg's World would not be possible without [Brython](http://brython.info), created by Pierre Quentel with the help of many collaborators.

I am also thankful to Google's development and support of [Blockly](https://developers.google.com/blockly/).

Remote collaboration is possible thanks to [Mozilla's TogetherJs](https://togetherjs.com/). However, this does not work with Blockly.

Reeborg's World has an interface available in Korean thanks to Kwangchun Lee and Muhun Kim.  Hopefully their contribution will inspire others to help make Reeborg's World available in even more languages.

[^1]: Please contact me if I have forgotten or misrepresented your contribution; my memory of what took place over the course of more than 13 years is not as accurate as I would like it to be.

