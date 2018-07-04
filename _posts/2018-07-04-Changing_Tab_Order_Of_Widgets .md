---
layout: post
title:  "Changing the tab order of widgets on a form"
date:   2018-07-04 17:30:00
img:
description: How to change the tab order of widgets on a form...
categories: [Python, Tkinter, Page, GUI]
---

As you might know, the tab order of the widgets on your form by default is determined by the order that you create them.  This isn't just in Page, but also Tkinter in general.

Many times, as designers, we will sketch out our forms on paper before we start but as we are actually building the form (either through Page or directly in code) something changes from the original sketch.  Adding a widget or moving it somewhere else will throw the tab order off.  Even if we stick to the original sketch, our end user may decide that they want things placed in a different order, even after they have "signed off" on the original design.

Tkinter provides us a very easy way to handle this kind of issue.  There is a command called `widget.lift()` that takes care of this.

Let's say that you have placed six entry boxes on your topmost form, laying them out something like this...

    Entry1                     Entry2
    Entry3                     Entry4
    Entry5                     Entry6
    
But later on, it is decided that the order should be:

    Entry1                     Entry4
    Entry2                     Entry5
    Entry3                     Entry6

Simply create a simple function with the name something like 'tab_order', create a list of each of the widgets that will get focus when the tab key is pressed, then iterate through the list calling  **widget.lift()** for each.

```python
def tab_order():
    widgets=[w.Entry1, w.Entry2, w.Entry3, w.Entry4, w.Entry5, w.Entry6]
    for wl in widgets:
        w1.lift()
```
Now, just before your form is shown at runtime, make a call to your tab_order function.

Both tab and shift-tab are supported by this.  Even if you are comfortable with your tab order upon your design, you might consider setting this up for all of your widgets that will accept focus, just in case.  Know what I mean?

And if you are using Page to do your design, if you are using version 4.14 or greater, you have a wonderful tool that will help you with this.  There is the 'Save Widget Tree' or (Alt-F) function, which will create a text file with all of the widgets on your form by name.  I've found this to be a wonderful tool to help me remember the alias names that I gave all of my widgets.  Of course, if you forget one of the widget names in your list, the order will be somwhat funky, those widgets NOT in the list are stuck at the bottom of the tab order.  Again, easy to fix, just add it into the list where you need it and re-run the program.

Since today is the 4th of July, it's a big day for those of us in the U.S.  So for us, Happy 4th of July.  For those living elsewhere in the world, Happy Wednesday!

_greg_