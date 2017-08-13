# Just the path, please

Either from the html selector, or using `World("Around 3")` select the world _Around 3_ and click on World Info. You will see the path taken by Reeborg as it accomplishes the task, presented as an animated gif. However, this animation will look quite different from the standard solution which looks similar to this static image:

![](/assets/around3.png)

By looking at an animated version of this image, a user can figure out:

1. when Reeborg turns, and with what sequence of orientations, since different images are used for each orientation;
2. how often Reeborg turns, since the path drawn is slighly off-centered which makes it easy to distinguish when a right turn is accomplished as three consecutive left turns;
3. when an object is dropped, since one can see the object **and** one can see that a number appears next to the object; this is both to give information as to the number of objects at a given location, as well as to distinguish between decorative objects and objects that can be picked up, as we have seen before.

### Getting a path with fewer hints

It is possible to get a path with fewer hints, as was done for the image included with the world _Around 3_:

![](/assets/around3_path.png)

1. We can use a completely transparent image for each of the robot orientations:

   ```python
   # using Python
   url="/src/images/transparent_tile.png"
   new_robot_images({"east": url, "west":url, "north":url, "south":url, "model":"invisible"})
   r = default_robot()
   r.set_model("invisible")
   ```

   Here, we have chosen "invisible" as the model for no particular reason - but the model must be the one specified in `new_robot_images`. `new_robot_images` is a Python function; you can use `help(new_robot_images)` to see its documentation.  Or, you can look at the more complete documentation for the Javascript equivalent `RUR.new_robot_images` which is callable from Python.

2. We can draw a thicker path which does not show any hint regarding the actual number of left turns required.

   ```python
   set_trace_style("thick")
   ```

   Note that, for world **Around 3**, we had also set the path to black using `set_trace_color("black")`.

3. We can also use the transparent image for the object.

   ```python
   RUR.add_new_thing({"name":"invisible", "url":url}) # same url as above
   RUR.give_object_to_robot("invisible", 1)
   put("invisible")   # instead of put() since Reeborg carries tokens as well
   ```

   Also, we use the following setting to not draw the number of objects at a given location, thus giving no indication that Reeborg is putting down an object.

   ```python
   RUR.state.do_not_draw_info = True
   ```

At the end, we reset the model name to the default value, `r.set_model("classic")` so that we can show Reeborg reaching the final position.

