---
title: "HammerSpoon — Workflow automation in Mac"
author: "Jordi Coscolla"
date: 2018-01-10T06:22:03.759Z
lastmod: 2020-02-11T21:51:03+01:00

description: "Today I want to talk about the tool I had used more in 2017, HammerSpoon has more usage in my computer than Chrome! It’s my window manager, my application launcher and basically can automate almost…"

subtitle: "Create your custom automation flows using HammerSpoon"

image: "/posts/2018-01-10_hammerspoonworkflow-automation-in-mac/images/1.jpeg" 
images:
 - "/posts/2018-01-10_hammerspoonworkflow-automation-in-mac/images/1.jpeg" 


aliases:
    - "/hammerspoon-workflow-automation-in-mac-87865ae6e7b2"
---

Today I want to talk about the tool I had used more in 2017, [HammerSpoon](http://www.hammerspoon.org/) has more usage in my computer than Chrome! It’s my window manager, my application launcher and basically can automate almost any task in it.




![image](/posts/2018-01-10_hammerspoonworkflow-automation-in-mac/images/1.jpeg)



So what is it? Hammerspoon makes accessible is just a wrapper of a bunch of obj-c API’s for accessibility, keybindings, windows, httpRequest, timers etc… and you can use them from a simple Lua program.

What can Hammerspoon do for you?

*   Do anything you want with the window positioning
*   Launch, kill, minimize any application in your mac
*   attach keybinding to specific functions
*   Detect when the laptop is connected specific network to launch some configuration
*   Event taping (receive and change the keyboard/mouse events)
*   Almost anything you can imagineAnd a tons of more things, look at the [documentation](http://www.hammerspoon.org/docs/index.html) is huge!

I just made my Hammerspoon configuration public in Github this week. so you can test hammerspoon without having to code anything at [https://github.com/kozko2001/hammerspoon](https://github.com/kozko2001/hammerspoon)

Also you can get more inspiration from the hammerspoon’s wiki [here](https://github.com/Hammerspoon/hammerspoon/wiki/Sample-Configurations).

Finally I get brave and create a small video showing going through my configuration and how HS work :D

Happy Development and happy Automation!
