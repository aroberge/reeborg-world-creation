# Extra module

Suppose that you would like to provide your students with additional functions or classes predefined. For example, you might want your student to use `turn_right()` without having to create such a definition themselves, or have a `RepairedRobot` which fixes many of the limitations of the default `UsedRobot`. You can do so by creating content for a special library module called **extra**. Once "installed" \(in the browser's memory\), students can use this content as though this was a standard Python module

```py
from extra import turn_right, RepairedRobot
```

Alternatively, you can do this code importation in the Pre editor which is executed just before the student's program: you can thus provide students with additional functions without requiring them to know and use an explicit import statement.

There are two ways you can create such a module:

1. From code written in a \(triple-quote\) string and executed using a special function. This is the recommended way as it requires fewer resources loaded using a third-party server \(see the appendix **About CORS**\).
2. From code written a normal Python module and publicly available on some server.

The preferred way is to use `RUR.extra_python_code(python_code)`. Have a look at

```py
World("worlds/examples/extra_python_code_test.json", "Extra 1")
```

and, as usual, click on **World Info** for details about the code.

The second method is to use the Python specific `install_extra(url)`\(without the `RUR` prefix\). An example is provided in

```py
World("worlds/examples/install_extra_test.json", "Extra 2")
```

This second example loads some code from a URL.

If you open the **Additional options** menu, at the very bottom there is an **Update extra** button; clicking on it should reveal the current content of the extra module if it was not already there.

### What about JavaScript?

JavaScript, at least as it currently exists, does not have a statement similar to Python's `import`.  However, by defining a global object \(as attribute to `window`\) you can make additional functions available for other programs executed with JavaScript.  For example, you may want to try adding the following:

```js
window.turn_right = function () {
    turn_left();
    turn_left();
    turn_left();
};
```

.After executing this program, you should be able to use `turn_right()` in any subsequent programs written in JavaScript.  You could include such definitions in the Onload part of a special world that student would load first, and then be able to use such definitions at any time in a given session.

## Contribute

Loading content from a third party site \(like from your server, or from [http://pastebin.com/](http://pastebin.com/), etc.\) requires the use of another server \(see the appendix **About CORS**\) which may not always be reliable. If you want to use the I will gladly host your content on my server in a special contributor area. Your content could include worlds files, custom images, or supplementary code for the **extra **module, which would all be more reliably retrieved from the main site.  However, I do ask that you provide such content under a license like CC-BY-SA or similar. Please contact me for more details.

