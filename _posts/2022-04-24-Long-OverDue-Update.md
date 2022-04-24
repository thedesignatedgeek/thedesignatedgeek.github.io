---
layout: post
title:  "Long Overdue Update April 24, 2022"
date:   2022-04-24 12:00:00
img: 
description: Yet Another Early Morning Update for September 12, 2020
categories: [Python, Page, Tkinter, GUI, Book, Full Circle Magazine]
sitemap: true
---

I recently sent my good friend Halvard a newer version of the PAGE Widget Demo that I'm working on for PAGE.  In it will be examples of how to use each and every widget that PAGE supports.  In one section of the demo, I show how to create hyperlink labels out of standard Tk Label widgets.

I wanted to have more than one hyperlink lable to show how easy it is create them.  I created one that links to Full Circle Magazine and one that links to the PAGE SourceForge page.  I wanted a third, but couldn't figure out what I could possibly link to that wouldn't be 

- Out of date too quickly or likely to have it's URL changed
- Very controversial or political
- Helpful in some small way or another 
- and one that I could remember the link

Out of despiration, I chose for the third this website.  Shameless self-promotion at it's worse, but there it is.  

I started putting each widget into it's own Labelframe to group each widget separately and allow for easy visual identification when a user looks at the demo.

So here is a quick image of what the Labelframe looks like for the hyperlink Labels

![Hyperlink Labels]({{"/assets/images/LinkedLabels.png" | absolute_url }})

One of the reasons that I send Halvard versions of my testing programs, is that he is very honest and upfront with me.  If something doesn't look right, he says so without worrying if I would be offended, which I wouldn't be.  Another reason is that he is ABSOLUTELY FANTASTIC about testing.  If I have something I've overlooked, he always finds it and points it out.

Well, he pointed out that I might not want to link to my homepage, since it has been, what seems like forever since I've updated.

Now you know why I put other tasks aside and did a quick update to the site and added this post.

Now, let's look at how to create the Hyperlink Labels.

In the PAGE designer, simply add a standard Tk Label widget where you want it to appear.  Enter the text that you want the Label to display.  You don't have to do anything like embed the URL in some strange way, just the text that you want to use to describe the Web page.  For example, if you want to link to Full Circle Magazine, just enter "Full Circle Magazine".  The URL portion will come later.  Since most hyperlinks are usually shown in blue, set the foreground colour to "blue" and for the font, set it to whatever you like.  I used the default font, bold and underlined.

That's it for the designer side of things.  Now you will add a few lines in the support module to support the link.  First, you need to import the webbrowser library (which comes with Python).

```python
import webbrowser
```

I usually put all my imports very close to the top of the support module.  Since the current version of PAGE is 7.3, you will already have a startup function added to the main function.

```python
def main(*args):
    '''Main entry point for the application.'''
    global root
    root = tk.Tk()
    root.protocol('WM_DELETE_WINDOW', root.destroy)
    # Creates a toplevel widget.
    global _top1, _w1
    _top1 = root
    _w1 = widgetdemo.Main(_top1)
    startup()
    root.mainloop()
```

You can see that the startup function call comes just before the last line of the main function.

Now somewhere in your startup function you would add a line like this...

```python
    _w1.Label10.bind("<Button-1>", lambda e: LabelLinkClick(1))
```

Of course, you would change the label alias to that of the label you are using, and the last part is the callback function.  Since I have three labels in my demo, I pass as a parameter a 1, 2 or 3 to denote which label was clicked.  I created two more lines like this, just changing the alias of the Label and the number of the url I want to use.

Finally, you need to create the callback function.

```python
def LabelLinkClick(*args):
    print('Into LabelLinkClick')
    for arg in args:
        print(arg)
    which = args[0]
    print(which)
    if which == 1:
        url = "https://fullcirclemagazine.org"
    elif which == 2:
        url = "https://sourceforge.net/projects/page/"
    elif which == 3:
        url = "https://thedesignatedgeek.xyz"
    webbrowser.open_new_tab(url)
```

The "number of the link" is passed in and will be available in the args list.  Since we are only looking for a single argument, it will be available as args[0].  I assign that to the variable ***which*** and then I use a simple ***if*** tree to determine the actual URL that will be called for that item.  There are three functions you can choose from.  **webbrowser.open(url)** which opens the webpage in the default browser if there is already one open, **webbrowser.open_new(url)** which will open the webpage in a new browser window and **webbrowser.open_new_tab(url)** which if a browser is already open, it will open the webpage in a new tab of that browser.

That's it.

Don has said that he would like to include my widget demo program in the next release of PAGE which will be 7.4.  We are beating the last of the bugs now, so hopefully the release will be soon.  I will also add a repository page for the demo and I will post the address here once it's complete.

Until we type again, Enjoy life, be safe and keep coding!



*Greg*
