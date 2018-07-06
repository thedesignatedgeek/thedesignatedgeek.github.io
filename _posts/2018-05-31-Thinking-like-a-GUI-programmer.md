---
layout: post
title:  "Thinking like a GUI programmer in Python"
date:   2018-05-31 06:00:00
img:
description: Thinking
categories: [Python, Page, GUI, Tkinter, center form]
sitemap: true
---

As I think back on my career as a programmer I realize that my entire career has always included being a mentor as a major component of my work.

As far back as my first corporate programming job, I was taking the tools that I used on a daily basis and repackaged them as a tool kit and shared them with other programmers on bulletin boards (this was in the days long before the Internet). Shortly after that, I started writing articles with a long distance friend about Modula-2, again sharing tools and tips that I had written simply to make my programming life easier.

In those days, everything I did was based on DOS. Windows didn't exist yet. Then we mostly wrote programs that were flat text based, but right before Windows entered the scene, there were toolkits that allowed programmers to make pseudo-GUI coloured forms.  Visual Basic for DOS had just come out and was taking the programming world by storm. Then Windows came into existence, and the rest is history. (Yes, I'm ignoring the Apple computers here.)

Now, between Page/Tkinter, QT and wxPython, we have a number of options to take our Python programs into the GUI world, making it easier for the user to interact with our programs. It is our job to think about the way the user will ultimately use our program to do their job and try to make it as efficient and somewhat enjoyable. It doesn't matter if that end user is someone on the Internet that you will never see or hear from, a fellow employee in your company, your wife or family members or just yourself. The end product needs to be easy and functional. Here are some thoughts on how to make that happens.

Remember the phrase, 'first impressions are everything'? That's true in our interactions with other people, but it is equally true for a program. The first full screen that a user sees will colour their mindset as to whether they like your program or not. We spend a great deal of time on this one fact alone. Something we often forget about is where the window shows up on the screen. If the window is not centred in the desktop, the user will more times than not, need to move it to keep their focus where it need to be to maintain their attention on the task the program is meant to accomplish, which takes time and effort and distracts from what they need to do. It is more comfortable for their eyes when the windows form is equidistant from the edges of the screen. No matter if it is a 17 inch screen on a laptop or a 34" monitor on the desktop. It just doesn't _feel_ right if it isn't centred. While many of us know this, when we are in the first stages of development, this is often something that we don't do right at the first. It's something that put on the list for being done "later on". And often that small simple step gets forgotten.

Next is something that I am horribly guilty of in my own programming. When I work with a Python GUI, I often rely on the terminal as my first line of feedback to the user, in this stage of programming that would be me, and the **_print()_** statement rules. I know in my heart of hearts that I should be using dialog boxes and notification bars to provide feedback, but it's something that I don't do often enough in the early development stage. Why? Because I also know in the back of my mind that the terminal window is ALWAYS there, so if I'm just providing information like "Could not open file", it's easier to dump it to the terminal via the **_print()_** command. And anyway, to dismiss that darned dialog box, requires me to move the mouse and click on the **_OK_** button, which takes time. Once again, like centring the screen, it's something that I will get around to eventually. It is something that should be done from the very beginning. It's a simple import statement once and a call to a function with (usually) two parameters. Not much more work than using the **_print()_** command.

Logging is also something we tend to put off until near the end of the project. It just seems easier that way. But it isn't really efficient to do it that way. Put the logging in early rather than relying on the terminal.

Consider this to make your life easier. Create a library module that you can simply import into your project that holds all of your code routines that you use (eventually) in most every program. Copy it into your development folder as one of your first tasks, so it's there when you need to create your distribution. Liberally comment it so that if someone needs to come behind you (or if _YOU_ need to come back to it 18 months into the future), they know what is going on. That will make it easy for you and like code completion snippets in your IDE, you will come to rely on them and wonder why you took so long to do it.

_Greg_




