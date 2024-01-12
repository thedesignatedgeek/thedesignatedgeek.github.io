---
layout: post
title: A Very small issue in PAGE 8.0
date: 2024/01/12 14:05:00
img: 
description: A small Issue in PAGE 8.0
categories: [Python, PAGE, Tkinter, GUI, Book, Full Circle Magazine]
sitemap: true
---

Greetings fellow beings.  Yet another post from Uncle Greggie (as I'm known on the PAGE Discord forum) currently located in a galaxy far far away called Central Texas. (Believe me, it REALLY feels that way sometimes!)

Yesterday (11 January, 2024), one of my friends with the screen name of Marvin contacted me with an issue that he was having after adding an "unsupported" theme into PAGE 8.0. When he tried to run the app he was working on, it would crash with (luckily) a rather verbose message.  I've pulled just the portion of the message that is really relevant...

```bash
File "/usr/lib/python3.10/tkinter/__init__.py", line 2601, in __init__
  self.tk.call(

_tkinter.TclError: unknown color name ""`
```

I mentioned to Marvin that the plastik theme was "officially unsupported" and he reminded me that no where did any of the documentation say that this theme (and the elegance theme) were unsupported.

I'll try to explain all the reasons that this had happen in my typical long winded manner.

When you startup PAGE 8.0, one of the first things it does is look in the /themes folder of the distribution for a file named 'themes_list.tcl'. This file contains a list of all the themes that PAGE should know about so it can populate the drop down so you can pick your theme for design time.

The /themes/themes_list.tcl file should look like this (as it ships in the original distribution)...

```tcl
set theme_dir $vTcl(VTCL_HOME)
set themes {
    clearlooks
    cornsilk-dark
    cornsilk-light
    notsodark
    page-dark
    page-legacy
    page-light
    page-notsodark
    page-wheat
    waldorf
}

foreach theme $themes {
    set filename [file join $theme_dir themes $theme.tcl]
    catch {source $filename}
}
```

This is not all the themes that are in the /themes folder though.  That folder also contains two "unsupported" themes named plastik.tcl and elegance.tcl .

In order to be able to use either or both of the extra themes, you need to edit the themes_list.tcl and add the name(s) of the themes you wish to add.  For this tutorial, I added both.  The last few lines of the list of themes in my file now looks like this...

```tcl
  ...
  page-wheat
  elegance
  plastik
  waldorf
}
...
```

Now when I start up PAGE, the two themes will be in the drop down.

PAGE then allows you to design your GUI with any of the themes in the list and switch at any time in the design process. This is one of the BIG benefits of PAGE 8.0.

In order to recreate the issue for you, I threw together a quick GUI using a simple TButton, a Labelframe and three TCheckbuttons. I selected the plastik theme, knowing there would be a problem, but not until I tried to run it.

So when I save and generate the two Python files, everything goes as expected. However, if I try to run the program either in a terminal window or from the support console run button, I get the following traceback...

```python
Running plastik1.py using python3 ...
Traceback (most recent call last):
  File "/home/greg/Desktop/pagetests/Page8.0/plastik1/plastik1.py", line 204, in <module>
    plastik1_support.main()
  File "/home/greg/Desktop/pagetests/Page8.0/plastik1/plastik1_support.py", line 25, in main
    _w1 = plastik1.Toplevel1(_top1)
          ^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/greg/Desktop/pagetests/Page8.0/plastik1/plastik1.py", line 69, in __init__
    ToolTip(self.btnExit, '''Exit''')
  File "/home/greg/Desktop/pagetests/Page8.0/plastik1/plastik1.py", line 120, in __init__
    self.msg = tk.Message(self, textvariable=self.msgVar, bg=_bgcolor,
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/greg/.pyenv/versions/3.11.4/lib/python3.11/tkinter/__init__.py", line 3473, in __init__
    Widget.__init__(self, master, 'message', cnf, kw)
  File "/home/greg/.pyenv/versions/3.11.4/lib/python3.11/tkinter/__init__.py", line 2628, in __init__
    self.tk.call(
_tkinter.TclError: unknown color name ""
Execution terminated.
```

Same as Marvin. 

When I saw Marvin's discord post, I knew what the problem was right off the bat. If you were to look at the GUI.py file, starting about line 16, you should see...

```python
...
import plastik1_support

_bgcolor = '#efefef'
_fgcolor = ''
_tabfg1 = 'black' 
_tabfg2 = 'white' 
_bgmode = 'light' 
_tabbg1 = '#d9d9d9' 
_tabbg2 = 'gray40' 
...
```

The offending line is this one (at line 19)...

```python
_fgcolor = ''
```

The reason for this is that the author of the plastik theme didn't include a default background colour. So when PAGE queries the theme looking for the "global" background and foreground colours, it gets the background, but since there is no foreground defined, PAGE simply puts an empty string for the colour.

This is easily fixed. Unfortunately I have, since PAGE 4.0 said "NEVER NEVER EVER EDIT THE GUI FILE BY HAND". So, I have to make this one exception JUST this once. 

Simply change "_fgcolor=''" to "_fgcolor='black'". 

Now the downside to the fix. If, for some reason, you have to regenerate your project, you will have to edit the GUI.py file again. Each and every time you regenerate your GUI.py, you will have to make that edit.

This is the same issue with the elegance theme. It also does not have a foreground colour set, so if you decide to use either the elegance theme or the plastik theme, you will run into this issue.

Now, the workaround for this is almost as simple and much easier on you. Design your program using the default theme. Do all your testing and then once you are ready to make your final save, change to the plastik (or elegance) theme, do your save and generate the Python modules. Then make the simple edit to the GUI.py file, replacing the empty string for the _fgcolor with "black" and you are good to go.

This is the reason that Don decided not to "officially" support either the plastik or the elegance themes at this time. So if you want to avoid this issue in your future projects, just don't use the plastik or elegance theme. However, if one of those themes REALLY speaks to you and you are moved to use them, just remember the simple "hack" and remember this is the ONLY time I will 'give you permission' to edit your GUI program. ;o)

I'm certain that this will be addressed in PAGE 8.1, in one way or the other. Until then, this is how you can use these two extra themes in your projects without too much issue.



Well, I've rattled on long enough for now.  Hopefully somewhere in this post, SOMETHING made sense.

Until next time, stay safe and stay creative!!!

Uncle Greggie
