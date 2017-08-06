# Loading worlds and other files

By now, you know that you can select a given world using the "html" select. It is also possible to do so from within a program.

### Selecting a world from the menu

Using the html selector, choose the default world **Alone**. Then, enter the following program and run it.

```py
World("Home 1")
move()
move()
```

The result will be as follows:

![](/assets/world_run_select.png)

Notice how the html selector has changed to "Home 1". If you move the dialog with the green bar indicating that the world Home 1 has been selected, you will see that the robot is at its starting position: the two `move()` instructions have been ignored.

Now, reload the world, and run the program again. This time, the `World()` instruction is ignored and the rest of the program is executed.

### Selecting a user's created world from the menu

In the previous section, you have created worlds that were saved in the browser. If you look at the html selector, you will see that their name is present, but that the background is yellow instead of white for the worlds included by default. I told you that I saved a world with the name `world_1` To select this world, I could use

```py
World("world_1")
```

and it would work just like it does for the worlds included by default. \(You should really try it with yours.\)

When you create a world, and attempt to save it in the browser with the same name as one of the worlds you have previously saved, a prompt window shows up asking you to confirm that you want to save the world under this name, thus replacing the old world. **This does not happen if you use the same name as a world included by default on the site.** Thus, you could save your own version of a world called "Home 3", for example, and the html menu would show two such worlds with the same name. If you want to select the world included on the site, you'd simply use

```py
World("Home 3")
```

If you wanted to select the world you had saved in the browser, you would need to add `user_world:` as a prefix:

```py
World("user_world:Home 3")
```

The addition of this prefix will work for any world you save in the browser, whether or not another world exists with the same name.

### Selecting a world from its URL

If you know the URL of a world, you can select it by the URL; for example, this example is for a world that is included on Reeborg's World site:

```py
World("worlds/examples/simple_path.json")
```

If you try this, you will see that the URL is added as the name in the html select element. This works also for worlds hosted elsewhere:

```py
World("http://personnel.usainteanne.ca/aroberge/reeborg/token.json")
```

However, this causes the html selector to become extremely wide.

![](/assets/long_html_select.png)

Furthermore, if you load many such worlds, it becomes difficult to identify them quickly. A better approach is to use a second argument for the `World` function:

```py
# World(URL, name)
World("worlds/examples/nice_path.json", "Nice path")
```

The name argument is what will be displayed in the html selector.  Later in the session, if needed, you will be able to load this world by simply using `World(name)`.

### Caveat

To load a resource, such as a world or an image, from a third party site, an intermediate server is used (see the appendix about CORS) and the result may not always be reliable.

A more reliable approach is for me to add your resources to the server where Reeborg's World is hosted. Contact me for more details.

### Sharing with a custom URL

If you want to share some information online about a particular world, you might be tempted to do something like the following:

> Go to [http://reeborg.ca/reeborg.html](http://reeborg.ca/reeborg.html). Then, enter `World("some_url")` in the editor and click run.

There is another method: the site will recognize a specially written URL. You can include information about

1. the programming mode/language
2. the human language for the interface
3. a URL pointing to a file containing the world definition
4. an optional name to display in the world select menu instead of the URL.

Using this method, the example above could have been written as

> Click on [http://reeborg.ca/reeborg.html?url=some\_url](http://reeborg.ca/reeborg.html?url=some_url)

As a concrete example, try

[http://reeborg.ca/reeborg.html?lang=en&mode=python&url=http://pastebin.com/raw/rGHudX7a&name=Desert](http://reeborg.ca/reeborg.html?lang=en&mode=python&url=http://pastebin.com/raw/rGHudX7a&name=Desert)

As a rule, if Reeborg's World is already loaded in your browser, you should use `World(URL)` instead of clicking on a link as this will minimize the bandwidth use.

