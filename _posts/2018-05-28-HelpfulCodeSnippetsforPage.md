---
layout: post
title:  "Helpful code snippets for Page"
date:   2018-05-28 08:15:00
img:
description: First in a series of code snippets for Page and Python.
categories: [Python, Page, Code Snippets]
sitemap: true
---

First, it is Memorial Day in the U.S. so Happy Memorial Day.

For months now, I've been keeping some tricks and tips in a text file that make programming User Interfaces easier.  For my Python UI work, I use Page which is a wonderful Drag-N-Drop GUI designer for Python that uses the Tkinter toolkit. Don Rozenberg has done a wonderful job creating and maintaining Page.  The latest version is 4.13, but 4.14 is due out any time. You can find it [here](https://sourceforge.net/projects/page/).

One of the standard "go to" functions I like to use is one that centers the form in the screen horizontally and vertically. Here is the code...

```python
def centre_screen(w, h):
    ws = root.winfo_screenwidth()
    hs = root.winfo_screenheight()
    x = (ws/2) - (w/2)
    y = (hs/2) - (h/2)
    root.geometry('%dx%d+%d+%d' % (w, h, x, y))
```

This should be placed in the yourprojectname_support.py file and called from the **init()** function. When you did your actual UI design in Page, you should have noticed and written down (at least somewhere temporary) the width and height of the topmost widget that makes up the form.

**Note:** For those who are not that familiar with Page, there are three files created for each "form" that is designed. These are:
  - filename.tcl
  - filename.py
  - filename\_support.py
 You should never hand edit the filename.tcl file and will hopefully not edit the filename.py file. The only file you should under normal circumstances is the filename\_support.py file.

You call the function like this:
```python
    centre_screen(300, 200)
```
where 300 is the width of the topmost form and 200 is the height of the topmost form.

I hope this function is helpful in your day-to-day coding.

_Greg_

