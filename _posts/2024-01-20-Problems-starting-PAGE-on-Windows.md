---
layout: post
title: Problems starting PAGE
date: 2024/01/20 06:00:00
img: 
description: An attempt to get to create a solution to the problem of starting PAGE on Windows
categories: [Python, PAGE, Tkinter, GUI, Book, Full Circle Magazine]
sitemap: true
---

Greeting Fellow Beings. Once again, I sit down and take time out of my projects to attempt to explain some of the problems in my universe.

One of the biggest things that Don and I have to deal with on PAGE is when users on Microsoft Windows can't get PAGE to run. Usually, the issue is in the page.bat file. Let me try to explain.

The PAGE batch file looks something like this when PAGE is initially installed...

```bash
 @start /min python3 "%~dp0page.py" %1 %2 %3
```

So let's take the command line apart a little bit and see what it is trying to do.

First, is the "@start". This tells Windows to start a new command prompt to run the commands that follow in.
Next, is the "/min". This tells Windows to minimize the command prompt while the commands run.
After that is "python3". This is the command to start Python using the command 'python3'. More on this later.
Then comes a really weird looking '"%~dp0page.py"'. The '%~dp0' part substitutes the current path and then provides 'page.py' as the name of the program or script to run. 
Finally are three parameters "%1 %2 %3". This allows you to start PAGE with parameters like the project name and/or the Preferences file to use when running PAGE session.

Normally, this works for most users. However, lately this has been a growing issue and is **USUALLY** because of the use of "python3" that is used to start the page.py file in Python. 

Back when Python 2.x was still a thing, you started Python with just the command "python". Then Python 3.0 was released and Python 2.x was still on most machines. There needed to be a way to be able to run both versions since Python 2.x was going to go away "soon" and people needed to migrate the existing programs over to Python 3 (which was no easy task, I can tell you). So the decision was made to keep "python" to start Python 2.x and "python3" to start Python 3.x.

That worked well for a long while and so PAGE started using "python3" in the page.bat file.

However, now that Python 2.x is all but gone, things are starting to change. When you install Python on Windows, there are two or three different ways and places to get Python. First is from python.org. The second place is from the Microsoft Store.

As a test, this morning I uninstalled both of the versions of Python from my Windows laptop, rebooted and then downloaded Python 3.11.4 directly from python.org.

That was really easy and didn't take very long. After the install, I rebooted the laptop again. Once the machine was running, I took to the command prompt (terminal window for Linux/Mac users) and asked for the version number of Python associated with the command "python -V".  So I typed...

```bash
python -V
```

and got the response

```bash
Python 3.11.4
```

Then I did a test for "python3"

```bash
python3 -V
```

and got back an empty response. So Python3 won't work on my system. If I leave the page.bat file as is, I would not be able to run PAGE. 

Then I tried a lesser known command. Just 'py -V'.

I got back the same response as the 'python -v', which was 3.11.4.

So what's up with just using "py"? Well, that started way back in Python 3.3 and it's called the **"Python Launcher for Windows"**. According to the python.org website https://docs.python.org/3/using/windows.html#launcher, 

> "The Python launcher for Windows is a utility which aids in locating and executing of different Python versions. It allows scripts (or the command-line) to indicate a preference for a specific Python version, and will locate and execute that version.

Unlike the PATH variable, the launcher will correctly select the most appropriate version of Python. It will prefer per-user installations over system-wide ones, and orders by language version rather than using the most recently installed version."

So if you had, for example, Python 3.7 and you wanted to use the launcher you could use just 'py' or 'py -3.7' to start Python. But it gets better.  Let's say you had two versions of Python on your Windows machine. You could do 'py --list'.  So if you had, for example Python 3.7 and Python 3.12.1, you would get back...

```bash
py --list
```

and the response would be...

```bash
 -v:3.7 *         Python 3.7 (64-bit)
 -V:3.12 *        Python 3.12 (64-bit)
```

You could also try the where command. For this one, I used my Windows Virtualbox instance. 

```bash
C:\development\PAGE\page8.0\test3>where python
C:\Users\gregg\AppData\Local\Programs\Python\Python312\python.exe
C:\Users\gregg\AppData\Local\Microsoft\WindowsApps\python.exe
```

Even though I only have Python 3.12.1 installed there, it gave me two listings. Why is that?

For some reason, there seems to be a stub installed in Windows in the '\local\Microsoft\WindowsApps\' folder that is named 'python.exe' but has a 0 bytes filesize. (There is also one named 'python3.exe' with 0 bytes as well. This explains the reason that when I try to run 'python3' the Microsoft store application opens up.)

So if the page.bat file doesn't work, try editing the batch file and replacing 'python3' with 'python' or simply 'py'.

Until next time, fellow beings, stay healthy and creative!

Uncle Greggie