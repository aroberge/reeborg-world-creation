# Worlds collections

You have created many interesting worlds that you want your students to use. Having to ask them to load each world independently by typing

```py
World("some_url", "Descriptive name")
```

can be both tedious and error prone.  However, there is a better way where you can replace the default html world selector by one of your own.  To see how this works, enter the following code in the editor and execute it:

```py
contents = [
    ["/src/worlds/tutorial_en/home1.json", "Home 1"],
    ["/src/worlds/tutorial_en/home2.json", "Home 2"]]
MakeCustomMenu(contents)
```

If you click on the html selector, you should see something like the following \(but with different names\):

![](/assets/make_menu.png)

You should recognize the first two worlds; their background is normally in white.  The yellow \(\#ff9\) background is used for worlds that are saved in your browser's local storage. The greenish-blue background \(\#9ff\) is used for **any **world whose URL converted to lowercase contains the string "menu". 

Instead of typing the example code above in the editor and running the program, load the following world:

```py
World("worlds/examples/make_menu.json")
```

This is what I used to create the image shown above.  The world file `make_menu.json` has the code to create the menu in the **Onload **editor.  Immediately upon loading this world, the code in the Onload editor was executed and a new menu was constructed, with the first world selected as the default.

To go back to Reeborg's World default menu, switch to a different language from the menu on the top right and switch back to your original language: the default menu for that language will be shown.

> In French, use either `MenuPersonnalisé` or `MenuPersonnalise` instead of `MakeCustomMenu`.

## Contribute

Loading worlds from a third party site \(like from your server, or from http://pastebin.com/, etc.\) requires the use of another server \(see the appendix **About CORS**\) which may not always be reliable. I will gladly host your worlds on my server in a special contributor area. Your worlds could include custom images, or supplementary code \(for the **extra **module\) which would all be more reliably retrieved from the main site.  However, I do ask that you provide such content under a license like CC-BY-SA or similar. Please contact me for more details.



