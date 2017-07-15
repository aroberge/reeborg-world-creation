# Creating a world: 3 different ways

While the menu driven **World editor**_ _ included in Reeborg's World makes it possible to create your own worlds, it is limited to create worlds with predefined objects. Furthermore, it only creates static worlds which are then interacted with through a user's program. A world creator may wish to introduce additional interactivity by changing the state of the world when a user's program has achieved a partial goal, like reaching a predefined position. The functions documented in this book are intended to give world creators all the flexibility they need to create their own worlds.

If you follow along the instructions described in this chpaterl, you will first create and save a world using the menu driven **World editing**\_ \_and then create the same world running a program that makes use of available methods instead. Finally, you will learn how to dynamically create a similar world using the **Onload editor**.

The world that we will create will:

* be much smaller than the default world
* have a wall blocking Reeborg's way
* have a house indicating a final position that needs to be reached.

And this is what  it will look like:

![](/assets/3x3_final.png)

It is important that you follow along, creating three different versions of the same world \(programming task\) so that you can understand the more complex examples provided later.



## 1. Using the menu-driven World editor

I strongly suggest that you follow along on the [Reeborg's World](http://reeborg.ca/reeborg.html) site. It is possible, even likely, that you will find at least some minor differences between the images included in this book and what you see on the actual site as I constantly tweak the site to make improvements. If the difference are so large as to make the instructions difficult to follow, please contact me so that I can update the information found in this book.

To access the menu-driven World editor dialog, you first need to click on the **Additional options** button.

![](/assets/reeborg_world.png)

Then, in the window that opens, click on the **Edit world** button.

![](/assets/edit_world_button.png)

This will open the menu-driven World editor \(and minimize the **Additional options** window that was previously opened\).

![](/assets/world_editor.png)

This window, like all other windows that can be opened in Reeborg's World as well as the Code editor can be resized by clicking and dragging on the sides or at the bottom, or can be moved on the screen by clicking on the top bar and dragging to a new location.

As you hover your mouse over the menu bar near the middle of the World editor window, various additional options are displayed.

![](/assets/menus_editor.png)

Make sure that the world that is currently selected is the default world named Alone, which has a robot in it at location \(1, 1\) and nothing else; it is the world displayed in the very first image shown in this chapter.

![](/assets/alone.png)

Then, in the World editor, click on **World dimensions**; a dialog similar to that shown below should appear.![](/assets/world_dimension.png)

Change the maximum values for x and y both to 3 and click **OK**; the world displayed should now be much smaller.![](/assets/3x3.png)

Next, hover over the **Goal **menu item and click on the **Robot **sub-menu: this allows us to choose a final position as a desired goal for the robot. By default, this final position can be indicated by one of three images.

![](/assets/position_image.png)

Click on the image of a house.  Then, in the small world, click on the grid location \(x, y\) = \(3, 1\). The world should now look as follows:

![](/assets/3x3_goal.png)

Finally, hover over the **Add **menu and click on **Wall**.

![](/assets/add_wall.png)

Then, click on the location of the vertical wall immediately in front of Reeborg; the result should be the following.

![](/assets/added_wall.png)

It is now time to save your work.  Click on the **Save world in browser** button.

![](/assets/save_world_browser.png)

In the dialog that appears, enter a name and click OK.  I chose **world\_1**; this is the name that is shown in the world selector at the top.

![](/assets/world_1.png)

Dismiss the **World Editor** by clicking on the X at the top-right corner.![](/assets/x_close.png)The World editor window should disappear and the appearance of the world grid should change, indicating that we are no longer in editing mode.

![](/assets/3x3_final.png)

The world has been saved in your browser's local storage; unless you explicitly delete it, it should be available next time you visit the site. However, you cannot share this world yet.  To do so, maximize the **Additional options** window by clicking on the bottom arrow next to the X at the right.

![](/assets/down_arrow.png)

Next, in the text field under the Edit World button, enter a file name \(I chose world\_1\); the ".json" extension will be automatically added reflecting the fact that a world is a simple javascript object stored in json format. After entering the name, click on the **Save world to file** button.

![](/assets/save_world_to_file.png)

Depending on your browser and your computer type \(Apple computers are acting very differently\), you may be given \(or not\) a choice of location to which you can save your file, or, if using Safari on an Apple computer, the content of the file might be displayed and you might have to explicitly save it using a standard Mac file dialog. I trust that you will be able to find the file that was saved.

_**That's it!**_  Using the World editor, you have created and saved a new world.  You might want to test it by writing a program that will make Reeborg reach its final destination.

## 2. Using a simple program

Explain the procedure

## 3. Using the Onload editor

Explain the procedure

