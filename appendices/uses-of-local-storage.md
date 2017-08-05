# Uses of local storage

As mentioned before, there is no login facility for Reeborg's World, and no information from the users is saved on the server. For convenience to the users, some information is saved in their browser's local storage, so that they can more easily resume their work when they return to the site. Here is a list of the information saved, so that it can be set immediately at the next session.

* The last language \(e.g., English, French\) used
* The last programming mode used \(Python, Javascript, Blockly-Py, ...\)
* The last robot model selected by the user from ![](/assets/available_models.png). Note that this is also retrieved each time a world is \(re\)loaded, in case a specific world had changed the robot model using some explicit code and without intervention by the user.
* The preference for "red" and "green" as set using 

```py
RUR.configure_red_green("red replacement", "green replacement")
```

* If a program was executed without syntax errors, so that frames could be recorded and displayed, the content of the main code editor and of the library are saved. If the mode selected is Blockly-Py or Blockly-Js, the current blocks defining the program are saved instead.
* The current world being used; this is only useful if the world is from the default menu for that language.
* Any world created and explicitly saved in the browser.  These are automatically added to the world selector \(html select\) when it is updated.
  * Each time such a world is saved, a new "delete" button is added to one section available by clicking on the **Additional options** button:

![](/assets/delete_local_storage.png)

