# Naming convention

> _**R.U.R.** is a 1920 science fiction play by the Czech writer **Karel **Čapek. R.U.R. stands for Rossumovi Univerzální Roboti \(Rossum’s Universal Robots\).\[1\] However, the English phrase Rossum’s Universal Robots had been used as the subtitle in the Czech original.\[2\] It premiered on 25 January 1921 and introduced the word "robot" to the English language and to science fiction as a whole._
>
> reference: [wikipedia:R.U.R.](https://en.wikipedia.org/wiki/R.U.R.)
>
> \[R. Pattis named his robot Karel, the inspiration for Reeborg, in honour of Karel Čapek.\]

Since the goal of Reeborg's World is to allow students to run their own programs, name clashes have to be avoided between functions created for Reeborg's World and those created by the student. The imperfect solution I have chosen is to try, as much as possible, to use a single global object or namespace, `RUR`, originally inspired by the 1920 science fiction play but which can stand for _**R**eeborg the **U**sed**R**obot_ and is also valid in French as _le **R**obot **U**sagé **R**eeborg_.

You have already seen this namespace being used in the first chapter with

```py
RUR.set_world_size(3, 3)
RUR.add_final_position("house", 3, 1)
RUR.add_wall("east", 1, 1)
```

You can see all the relevant functions for creating world \[add link here\]. Please note that there are likely more functions belonging to the `RUR` namespace than what is documented on that site.  As a general rule, you should not create additional functions belonging to this namespace.

## A simple pattern

To create interesting worlds without using the menu-driven editor, at the very least you need to know:

* The name of _things_
* **If** a _thing_ of a particular _type_ can be found at a given location
* How to **add** a _thing_ of a particular _type_ at a given location
* Possibly, how to **remove** a _thing_ of a particular _type_ at a given location.

The _**basic**_ naming convention follows the following pattern:

* `RUR.is_TYPE(name, x, y)`
* `RUR.add_TYPE(name, x, y)`
* `RUR.remove_TYPE(name, x, y)`

  Possible value for `TYPE` include the following:

  * `background_tile`
  * `bridge`
  * `decorative_object`
  * `object`
  * `obstacle`
  * `overlay [todo: implement this]`
  * `pushable`
  * `wall`

Thus, we could have:

* `RUR.is_background_tile("grass", 3, 4)` would indicate whether or not a `"grass"` tile was used as a background tile at location `(3, 4)`.
* `RUR.add_object("token", 2, 5)` adds a `"token"` as an object \(that can be picked up\) at location `(2, 5)`.
* `RUR.remove_obstacle("vertical_fence", 1, 5)`; etc.

As we saw with `RUR.set_world_size(3, 3)`, some functions do not follow this pattern. A few other cases, such as "final position" which we saw, also have only one of the three basic methods \(add/is/remove\) but not the others.

## When 3 is not enough

In some cases, the basic three arguments, `name`, `x`, and `y`, are not sufficient.  To deal with such cases in a general way, a fourth argument can be added; this argument will be a Python **dict** or, if using Javascript, a simple object. Some specific examples are provided later.

## Available _things_ and general help

To view what _things_ are available, you can execute a program with a single line of code.

```
RUR.show_all_things()
```

If you are using a non-English version, an extra column is shown using the translated name \(if available\); this translated name is the one that would be needed in a user-written program, e.g. `prend("feuille")` instead of `take("leaf")`.

Instead of entering this line in the editor, you can use the Python REPL mode

From either the editor or the Python REPL, you can also get some _help_:

* To list all available Python functions, classes, etc, simply enter `help()`.
* To get help about a particular function, for example `move`, enter `help(move)`
* To get a complete, up to date version of every Python function available in the English version, enter

  ```python
    import reeborg_en
    help(reeborg_en)
  ```

  You can use `reeborg_fr` to get the corresponding French version. Note that this help system is specific to Python and does **not** include the available Javascript functions prefixed by `RUR.`

## Note about the word "thing"

In Reeborg's World, the word _object_ has been used for many years to describe "things" with which Reeborg can interact and is used in some functions like `object_here()`. The word _type_ refers to a certain classification of "things" described above. The word _artefact_ is used in the code for many basic functions. If these were not already used, I would have chosen any one of them instead of using "thing", as in `show_all_objects()` instead of `show_all_things()`... If you have any suggestion for a better term than "thing", feel free to contact me.

