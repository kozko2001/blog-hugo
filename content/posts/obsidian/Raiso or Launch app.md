
---
title: Run or Raise 
date: 2022-09-23 00:00:00
---
---

Run-or-Raise shortcuts, are global shortcuts for focusing the window on an app (if already running) or launching it.

I have to confess I got addicted, it feels extremely natural to just have a chord (Ctrl-Cmd-Option) and some other key to bring whatever you need in your screen. No more Cmd-Tab-Tab-Tab-Tab until find the app you want.

In mac, I get there with [Hammerspoon](https://www.hammerspoon.org/). It's just a lua embed runtime that give you all the accessibility API in MacOSX. You can find [my configuration](https://github.com/kozko2001/hammerspoon/blob/99937317a3ee70081b41ef8df57acb5b8563344e/init.lua#L120)

In linux, there is so much windows manager etc... that it's a bit more complex, but if you can bind a shortcut to a command line executable (which all wm's allow that). you can use [jumpapp](https://github.com/mkropat/jumpapp) specifying the name of the window, or the executable to run if the window is not found.
