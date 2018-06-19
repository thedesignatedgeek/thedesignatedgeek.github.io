---
layout: post
title:  "The Checkbutton Conundrum"
date:   2018-06-19 05:15:00
img:
description: Checkbutton Widgets don't seem to update correctly
categories: [Python, Page, Tkinter, Widgets]
---
Recently, I wanted to have an Tkinter entry widget change from a disabled state, where no editing is allowed, to a normal state that allows for editing.  At first thought, that seems very simple.  A Checkbutton widget can be used to toggle the Entry widget from state=tk.DISABLED to state=tk.Normal. However, that isn't quite the case. I'll get into that in a moment.

I used to use Bind rather than Command to respond to button clicks. Bind, by default, always wants to pass an event object to the callback function and I thought that wasn't a bad thing. If I didn't need it, I could simply ignore it in my code. Bind also lets you send additional parameters to the callback function when you need it. Command, however doesn't allow for passing the event as a parameter AND there are some widgets that don't provide a Command option, like the Combobox or Entry widget.

So I put a Checkbutton widget into my GUI and set a bind to Button-1. In the callback function, I simply monitored the Checkbutton variable to see if it was a '1' (checked) or a '0' (unchecked) and set the Entry widget state appropriately. Easy enough, right?

But Nooooooo. When I tested the program, the Checkbutton was unchecked at startup and the Entry widget was in a disabled state. Just what I wanted. When I clicked on the Checkbutton, the check appeared as planned, but the Entry Widget stayed disabled. Confused, I clicked the Checkbutton again, clearing the check and the Entry widget changed to a Normal state! I toggled the Checkbutton again and as before, things happened in reverse. I checked my code and everything was correct.

Frustrated, I searched the web, but couldn't find anything that applied. Not be bested by a program that I wrote, I went into _"fix it now and understand it later"_ mode. I commented out the bind statement and use the command option to link to the callback function. When I ran the program again, everything worked as expected. Frustrated, but placated for the moment, I let it go and continued writing the rest of the program.

Once done, I decided to work on another project that required multiple  Checkbutton widgets but this time, I absolutely needed the data from the event to be passed into the callback function. And as expected, I ran into the same issue as before. However, this time, I took the time to try one more thing. Rather than using the `<Button-1>` event, I used the `<ButtonRelease-1>` event. It worked!

It seems that when using the `<Button-1>` event on a Checkbutton widget (or on a Radiobutton widget), the callback code gets run IMMEDIATELY, before the widget changes state. However, the `<ButtonRelease-1>` changes the state of the widget first, then runs the callback code.

This is a Tkinter issue (NOT an issue with Page) and can even cause issues with normal Button widgets. I found a long time ago that if you have a Button that you bind to `<Button-1>` and within the callback function you call a dialog box, like the askopenfilename filedialog, the button will visually stay in a clicked down mode and never returns to the "up" visual mode.

So, in a nutshell, any widget that changes state that you need the event data to be sent to your callback function, use the `<ButtonRelease>` event, instead of the `<Button-1>` event.

_greg_


