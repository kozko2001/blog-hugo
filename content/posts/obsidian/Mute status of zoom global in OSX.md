
---
title: Mute status of zoom in the OSX bar
date: 2021-09-01 00:00:00
---
---

Lately I have a bunch of meeting and I like to do "other" stuff while listening, and also be able to contribute at the speed of a single key-stroke.

Zoom already has this functionality, Cmd-Shift-A is  the keystroke for toggling mute/unmute state. By default it's not set to be globally, but you can make globally in zoom settings.

So that's it? sadly no, since I don't have zoom in the front of the screen, I don't know when I am already muted or not...

I found this article on how to [setup a mute indicator for zoom in hammerspoon](https://developer.okta.com/blog/2020/10/22/set-up-a-mute-indicator-light-for-zoom-with-hammerspoon). Since I am already using hammerspoon as my "window tiling" and for launching apps, I did a small tweaks to poll the information of zoom into the osx bar. 

you can see the integration here: https://github.com/kozko2001/hammerspoon/commit/99937317a3ee70081b41ef8df57acb5b8563344e
