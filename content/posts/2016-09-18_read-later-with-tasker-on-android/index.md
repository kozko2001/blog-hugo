---
title: "Read later with Tasker on Android"
author: "Jordi Coscolla"
date: 2016-09-18T03:11:35.347Z
lastmod: 2020-02-11T21:48:46+01:00

description: ""

subtitle: "There are a bunch of services to store all the links you go through the day, yeah these links that seems interesting but you don’t have the…"

image: "/posts/2016-09-18_read-later-with-tasker-on-android/images/1.png" 
images:
 - "/posts/2016-09-18_read-later-with-tasker-on-android/images/1.png" 
 - "/posts/2016-09-18_read-later-with-tasker-on-android/images/2.png" 
 - "/posts/2016-09-18_read-later-with-tasker-on-android/images/3.png" 
 - "/posts/2016-09-18_read-later-with-tasker-on-android/images/4.png" 
 - "/posts/2016-09-18_read-later-with-tasker-on-android/images/5.png" 
 - "/posts/2016-09-18_read-later-with-tasker-on-android/images/6.png" 
 - "/posts/2016-09-18_read-later-with-tasker-on-android/images/7.png" 
 - "/posts/2016-09-18_read-later-with-tasker-on-android/images/8.png" 


aliases:
    - "/read-later-with-tasker-on-android-cd15478d444c"
---

There are a bunch of services to store all the links you go through the day, yeah these links that seems interesting but you don’t have the opportunity to read them and appreciate all what the author share in the post.

We all have in this position and there is two possible outcomes in these situations.

1.  You loss this link forever, don’t store anywhere and think that if it was really life changing will popup again.
2.  Use a service like Pocket, and store all there

I have been a pocket user for a lot of time, but always had to remember to open it to see what to read next and if not, well all the links accumulate on the inbox and what basically happens is that a bunch of them I never opened again.

Lately I have tested a new approach, a much basic one, I’m a really happy user of SimpleNote, Is my first open app (even before than chrome) and use it to take notes all the day in front of the computer.

So I made a small service that allow me add the read-later links to a note in SimpleNote.

There are a bunch of ways of doing this, but I want to have fun hacking a bit with my android phone and Tasker.

Tasker is an App that allow you to do certain actions when some events occur on your device. Like **whenever** the wifi connects at work **then** put the ringtone in silence.

The basic idea of what the system does is each time we share from chrome the link, we will make a POST request to our service that will store the link information in a specific note on simplenote.

#### Step 1: Configure Tasker to intercept the Share action in Android

For this we can use AutoShare, AutoShare is a plugin for Tasker and will appear on the possibles apps to share the link.

Just intall AutoShare from [here](https://play.google.com/store/apps/details?id=com.joaomgcd.autoshare&amp;hl=en)




![image](/posts/2016-09-18_read-later-with-tasker-on-android/images/1.png)



Click on Manage Commands




![image](/posts/2016-09-18_read-later-with-tasker-on-android/images/2.png)



And create a new command, we can name it anyway we want (I named it bookmarks), one think to know is that if you want to use AutoShare for more things you will need to pay for the app.

#### Step 2: Configure Tasker

Install [Tasker](https://play.google.com/store/search?q=tasker&amp;c=apps&amp;hl=en) and on the profiles tab, click on the + button and then Event, then Plugins and finally on AutoShare




![image](/posts/2016-09-18_read-later-with-tasker-on-android/images/3.png)





![image](/posts/2016-09-18_read-later-with-tasker-on-android/images/4.png)





![image](/posts/2016-09-18_read-later-with-tasker-on-android/images/5.png)





![image](/posts/2016-09-18_read-later-with-tasker-on-android/images/6.png)



Now on tap on the configuration and the autoshare app will open, just click on the Ok button




![image](/posts/2016-09-18_read-later-with-tasker-on-android/images/7.png)



we can press the back button on the tasker app (Yeah tasker is a really powerful tool but it doesn’t have the best experience for users)

Click on “New Task”

Click On the + button, And select the **Net** button, and then the **Http Post**

Finally just insert the domain name where the backend code will be stored and in the data section add “**%astext**”




![image](/posts/2016-09-18_read-later-with-tasker-on-android/images/8.png)



#### Step 3: Backend code

The code is really basic, you can find it in my github account [https://github.com/kozko2001/bookmarks](https://github.com/kozko2001/bookmarks)

There are the instructions to deploy but if you are using docker is really easy, just a docker build, and then a docker run.

Now whenever you share your link with the AutoShare app on the device the note will be updated at the moment :)

Happy hacking.
