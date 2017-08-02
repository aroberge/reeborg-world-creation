## Checklist for a good programming environment

In their 1997 paper, [Mini-languages: A Way to Learn Programming Principles](http://www.contrib.andrew.cmu.edu/~plb/papers/minilang.html),[^3] Brusilovsky _et al._ provide an overview of the mini-language approach to teach programming and mention many requirements that they consider important for a successful application of a mini-language. Here is a list of these requirements together with an explanation as to how Reeborg's World attempts to meet each requirement.

* _The mini-language should be **simple **in both its syntax and semantics._

  * Using the simple function based approach, with instructions like `move()` and `turn_left()`, and using Python as the basic programming language \(limiting to simple constructs\) meets this requirement - especially if one initially uses the fake Python keyword, `repeat n:` that I added to replace the standard construct `for variable in range(n):`; see the section on `repeat` for more details.

* ... _most operations performed by the actor should make visible changes in the microworld represented on the screen._

  * This is the case with the robot world graphical representation.

* ... _any mini-language command can be executed in both navigation mode \(single command execution\) and programming mode \(complete program execution\)_.

  * With the Python REPL, single command executing is made possible; complete program execution is accomplished by using the code editors or the Blockly environment.

* _It should contain a mechanism for creating abstract instructions \(procedures\)._

  * This is done using Python's `def` or Javascript `function`. It is also supported by the Blockly interface.

* _The procedures designed for a particular problem can be later re-used for solving subsequent problems._

  * This is supported by providing a user's **library **when programming with Python.

* _The learning should be supported by a good programming environment. Such an environment should keep both the microworld and the student program visible on the screen._

  * This is how Reeborg's World has been designed to look from the very beginning - including its desktop predecessor, RUR-PLE.

* _The program should typically be executed one instruction at a time, while the interpreter highlights programming constructs in the source code as they are being executed and the effect is simultaneously shown in the microworld._

  * This is available by default when using Python as the programming language. One can step through the program one instruction at a time and even step backwards if needed.

* _The interpreter should also provide visualization for those concepts of the language that are not visualized by the microworld. Important features include visualization of variables and the stack of subroutine calls._

  * With the exception of the visualization of the stack of subroutine calls, this is possible with the somewhat experimental "watching variable" feature.

![](/assets/watch_vars1.png)

* _A good mini-language should be complemented with a good set of attractive and meaningful problems for students to solve._

  * I completely agree. Reeborg's World include a small set of such programming tasks \(worlds\) ... and I am counting on you to increase the number of such tasks available! :-\)

I do have one disagreement with the traditional mini-language approach: I believe that students can be more motivated to learn programming if they are using a "real" programming language rather than an artificial and limited one made up only to teach basic programming concepts.

[^3]: Brusilovsky, P., Calabrese, E., Hvorecky, J., Kouchnirenko, A., and Miller, P. \(1997\) _Mini-languages: A Way to Learn Programming Principles. Education and Information Technologies_ 2 \(1\), pp. 65-83.

