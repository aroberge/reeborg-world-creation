# A brief word about Blockly

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

## Loading an example

Using Blockly should be fairly intuitive, and I currently have no plan to
describe how to do so in this book.
However, loading an existing world saved with Blockly code may
not be obvious, and since we are on the topic of Blockly, I thought it would be
appropriate to include the information here.

To load a blockly example, enter the following in a code editor and run it:

```py
World("worlds/examples/square_blockly.json", "square")
```

This world was saved with blocks included, something which has to be selected explicitly each time you want to save a world; how exactly to do so will be explained later.

![](/assets/save_with_blocks.png)

Upon loading the world, the mode will change to the Python version of Blockly and, unless you already had exactly the same blocks in the Blockly work area as those included with the world, you will be greeted by the following:

![](/assets/replace_blockly.png)

Click on **Replace existing blocks**; you should see the following in the work area:

![](/assets/repeat_blockly.png)

At the very top, toggle the **Keep editor** visible option.

![](/assets/editor_visible.png)

The editor is in read-only mode \(i.e., you cannot change its content\); this is indicated by the striped background and is the same colour scheme used in the **World info** window. Note that you can move aside the editor so that you can view its content and view the blocks in the Blockly workspace at the same time.

### Running the code

Running the code is done the usual way, by clicking on the **run** button:

![](/assets/run_button.png)

You can do so either with the editor visible or not. After you click the run button, the code gets translated into the Python equivalent[^1] and copied into the editor \(still in read-only mode\): the content of the editor is what gets executed by the normal interpreter.

The reason for having the editor in read-only mode is that one could write Python \(or JavaScript\) code for which there isn't any code block equivalent; in this case, there would not be an equivalence between the program written with blocks and the program in the editor. The assumption I have made is that, when students are ready to write code in the editor, they can forego the Blockly mode and use a "standard" text-based mode only.

> **\[info\] Visual design conundrum**
>
> I am not a designer and have struggled to come up with a consistent look-and-feel for the site. I have done this over the course of many years \(starting approximately in 2009\) and, as some people have pointed out, in the meantime the "flat css" style has become the norm: Reeborg's World looks dated.
>
> One of my early goals was to have the coding area be very distinct from the world; this, and the goal of having a consistent colour scheme, is what led me to create a style for the editor with a dark blue background.  For consistency, I decided that any code that would appear \(like in the **World info**\) should look somewhat similar, with the strings, keywords, functions, etc.,  using the same colour scheme as in the code editors. However, I wanted to have a visual difference between code that could be edited by the user and code that could not be edited and was shown for information only. The choice I have made has been to use a solid background for code that can be edited
>
> ![](/assets/code_not_striped.png)
>
> and a striped background for code that cannot be edited
>
> ![](/assets/code_striped.png)
>
> The difference between the two is probably too small to convey effectively the information to the user. I have tried to use more visible differences but have not been able to come up with something that looked acceptable.
>
> **If you have any suggestion to offer, please do not hesitate to do so.**

[^1]: The code could have been translated into JavaScript instead of Python, if the option of using the Blockly-JS mode had been possible, which it is not for this particular world.


