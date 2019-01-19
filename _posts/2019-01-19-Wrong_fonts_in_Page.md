---
layout: post
title:  "Wrong fonts in Page"
date:   2019-01-19 03:15:00
img:
description: Wrong fonts on the Page windows
categories: [Python, Page, Tkinter]
sitemap: true
---

You just downloaded the latest version of Page, got it setup and started it.  You are presented with a main menu that looks like this...

![Weird Font]({{"assets/images//PAGE-_078.png" | absolute_url }}  "Weird Fonts in Page")

Now, you know that at least one of the previous versions looked correct, so what changed?  Well it isn't Page.

Do you have Anaconda3 installed on your system?  That's the problem.  Let's delve into the configure process and see what happens.

Wheh you set up a new version of Page, you unpack the .tgz file into a folder, then run ./configure which looks through your system for a compatible Tcl wish file and then readys the page file.  Let's take a look at part of the configure script...

```tcl
findwish( ) {
WISHES=" \
	wish8.6 \
	wish8.5
"

# The sed command replaces ":" with " " .
DIRS=" `echo $PATH | sed -e 's/:/ /g'` \
    /opt/ActiveTcl-8.6/bin \
    /usr/local/bin	\
	/usr/bin	\
	/bin		\
	/opt/local/bin	\
	/opt/bin	\
    /opt/tcltk/bin 	/opt/bin	\
    /opt/tcltk/bin 
"
```

This is farily straight forward.  But here is what happens to me...

```tcl
#!/bin/sh

PATH_TO_WISH=/home/greg/anaconda3/bin/wish8.6
PAGE_HOME=/home/greg/Downloads/Page-419/page

export PATH_TO_WISH
export PAGE_HOME

exec ${PATH_TO_WISH} ${PAGE_HOME}/page.tcl "$*"
```

Instead of pointing to the ActiveTCL wish (which I DO have installed), it's pointing to a wish file in the anaconda3 folder.  So that's the problem.  

I'm pretty sure that I have a copy in the /usr/bin folder, but I check just in case...
```tcl
greg@slartibartfast:~$ ls /usr/bin/wish*
/usr/bin/wish  /usr/bin/wish8.5  /usr/bin/wish8.6
greg@slartibartfast:~$ 
```

Now I know for sure that I have another wish in the /user/bin folder, so I change the first line to that.

```tcl
# PATH_TO_WISH=/home/greg/anaconda3/bin/wish8.6
PATH_TO_WISH=/usr/bin/wish8.6
...
```

And then I run Page...

![The Right Fonts]({{"assets/images//PAGE-_079.png" | absolute_url }}) 

Now everything is the way I like it.  All is good in the world and I can go back to work.

So just remember this little tip and if it ever happens to you, you'll know how to fix it in less than 3 minutes.

*greg*