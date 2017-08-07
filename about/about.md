# About Reeborg's World

I am using the words _**Reeborg's World**_ to mean three different things.

* [Reeborg's World \(main site\)](http://reeborg.ca) is a website I designed to help people to learn programming. It includes a Python tutorial \(which is in serious need of updating\) available in English, French and Korean. 
* The main feature of the site, and the one primarily referred to in this document, is a single-app page which is usually what I mean when I write [Reeborg's World](http://reeborg.ca/reeborg.html). 
* Finally, I sometimes refer to Reeborg's _**world**_ \(lower case _w_\) as a single programming task.

## About Reeborg

![Photo courtesy of Andy Judkis](/assets/reeborg_judkis.jpg)

Here is how I describe Reeborg and its world to students:

_Not so good programmers state that “bugs” are not really bugs but that they are “features” of their programs. **You **are going to be a good programmer, unlike the maker of Reeborg, whose program is littered with bugs._

1. _Reeborg has an oil leak. Oil leaks are damaging for the environment and inconvenient for Reeborg who must replenish its supplies when it’s not busy accomplishing tasks. The maker of Reeborg claims that it is a feature, as it enables you to follow Reeborg’s path, just like any programmer can learn to “trace” a program; Reeborg disagrees. You will learn how to fix Reeborg’s leak later. More advanced techniques to trace bugs, like using what is known as a **debugger**, are beyond the scope of what can be done here._
2. _Reeborg’s steering mechanism is not handled properly by Reeborg’s program: it can only turn left. The maker of Reeborg, once again, claims that this is a feature as it presents you with an opportunity to learn about functions. Once again, Reeborg disagrees. You will soon learn how to program a **workaround solution**, enabling Reeborg to turn right, although in a wasteful fashion. Much later, you will learn how to truly fix Reeborg so that it can turn right just as easily as it can turn left._
3. _Reeborg has a compass, which makes it possible to find out which direction it is facing. Unfortunately, yet again, the program that enables Reeborg to get the information from the compass has a bug: it only tells Reeborg if it is facing North ... or not. Once again, you will first learn how to implement a workaround solution and later how to fix permanently Reeborg and get rid of what its maker calls a “feature”. Learning to do so will require you to learn how to use the _`return`_ keyword in either Python or JavaScript._
4. _Reeborg can see if a wall is blocking its way, and can also turn its head to the right to see if there is a wall there. However, a software “glitch” \(which is another weasel term that software manufacturers use to avoid having to say that their product has a bug\) prevents Reeborg’s program from properly registering a wall when it turns its head left. You will be able to fix this too._

_Sometimes to find the cause of bugs, it can help to break the normal flow of the program. To this end, you may do one or more of the following, some of which will be explained later:_

1. _You can pause program as it is running by pressing the **pause **button. This is similar to what people refer to as setting a **breakpoint **in a computer program._

2. _Instead of actually pressing the pause button, you can type in the instruction _`pause()`_ at any point inside a program and Reeborg will pause, awaiting your instruction to continue. _

3. _You can step through a program, one instruction at a time, by pressing the "execute one instruction and pause", or **step **button. By default, the line about to be executed is highlighted; you can turn off the highlighting by clicking on a button above the code editor._

4. _You can change the speed of execution at any point inside a program using the _`think()`_ command._

5. _You can have Reeborg write some information at any given point inside a program using the _`print()`_ function. _
6. _Finally, you can stop a program at any point by pressing the **stop **button; this unfortunately may not work if you create what is known as an infinite loop, outside of Reeborg’s control. If worse comes to worst, you can always just reload the web page._



