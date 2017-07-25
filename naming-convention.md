# Naming convention

> _**R.U.R.** is a 1920 science fiction play by the Czech writer **Karel **Čapek. R.U.R. stands for Rossumovi Univerzální Roboti \(Rossum’s Universal Robots\). However, the English phrase Rossum’s Universal Robots had been used as the subtitle in the Czech original. It premiered on 25 January 1921 and introduced the word _**robot **_to the English language and to science fiction as a whole._
>
> reference: [wikipedia:R.U.R.](https://en.wikipedia.org/wiki/R.U.R.)
>
> \[Note that Karel the robot, the inspiration for Reeborg, was thus named by R. Pattis in honour of Karel Čapek.\]

Since the goal of Reeborg's World is to allow students to run their own programs, name clashes have to be avoided between functions created for Reeborg's World and those created by the student. The imperfect solution I have chosen is to try, as much as possible, to use a single global object or namespace, `RUR`, originally inspired by the 1920 science fiction play but which can stand for _**R**eeborg the **U**sed **R**obot_ and is also valid in French as _le **R**obot **U**sagé **R**eeborg_.

You have already seen this namespace being used in the first chapter with

```py
RUR.set_world_size(3, 3)
RUR.add_final_position("house", 3, 1)
RUR.add_wall("east", 1, 1)
```

You can see all the relevant functions included in the [Application Programming Interface \(API\)](http://reeborg.ca/api/RUR.html) for creating world. Please note that there are likely more functions belonging to the `RUR` namespace than what is documented on that site.  As a general rule, you should not create additional functions belonging to the RUR namespace.

## A simple pattern

To create interesting worlds without using the menu-driven editor, at the very least you need to know:

* The name of _things_
* **If** a _thing_ of a particular _type_ can be found at a given location
* How to **add** a _thing_ of a particular _type_ at a given location
* Possibly, how to **remove** a _thing_ of a particular _type_ at a given location.

The _**basic**_ naming convention to do such actions follows the following pattern:

* `RUR.is_TYPE(name, x, y)`
* `RUR.add_TYPE(name, x, y)`
* `RUR.remove_TYPE(name, x, y)`

  Possible values for `TYPE` include the following:

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

## When three is not enough

In some cases, the basic three arguments, `name`, `x`, and `y`, are not sufficient.  To deal with such cases in a general way, a fourth argument can be added; this argument will be a Python **dict** or, if using Javascript, a simple object. Some specific examples are provided later.

## Available _things_ and general help

To view what _things_ are available, you can execute a program with a single line of code.

```
RUR.show_all_things()
```

![](/assets/show_all_things_en.png)

If you are using a non-English version, an extra column is shown using the translated name \(if available\); this translated name is the one that would be needed in a user-written program, e.g. `prend("feuille")` instead of `take("leaf")`.

![](/assets/show_all_things_fr.png)

Instead of entering this line in the editor, you can use the Python REPL mode; this is something I find useful when I look things up as it leaves the code in the editor unchanged.

![](/assets/show_all_things_repl.png)

From either the editor or the Python REPL, you can also get some _help_:

* To list all available Python functions, classes, etc., simply enter `help()`.
* To get help about a particular function, for example `move`, enter `help(move)`
* To get a complete, up-to-date version of every Python function available in the English version, enter

  ```python
    import reeborg_en
    help(reeborg_en)
  ```

  You can use `reeborg_fr` to get the corresponding French version. \[**Suggestion**: if you teach using a language other than English or French, I will gladly add a version in your own language ;-\)\] Note that this help system is specific to Python and does **not** include the available functions prefixed by `RUR.` With a few exceptions, if a function exists in Python \(e.g. `move()`\), there is one with the same name also available when using Javascript.

There is a separate function to show existing robot images:

```
RUR.show_all_robots()
```

## Note about the word "thing"

In Reeborg's World, the word _object_ has been used for many years to describe "things" with which Reeborg can interact and is used in some functions like `object_here()`. The word _type_ refers to a certain classification of "things" described above. The word _artefact_ is used in the code for many basic functions. If these were not already used, I would have chosen any one of them instead of using "thing", as in `show_all_objects()` instead of `show_all_things()`... However, even if you have a better suggestion, it is probably too late to make changes without annoying existing users.

