---
title: "Jenkins Pipelines — Tips And Tricks"
author: ""
date: 
lastmod: 2020-02-11T21:51:07+01:00
draft: true
description: ""

subtitle: "Jenkins is one of the most used CI systems. Allowing all the people involved with the project to have trust in the current state of the…"




aliases:
    - "/"
---

Jenkins is one of the most used CI systems. Allowing all the people involved with the project to have trust in the current state of the code. Each time a member of the team pushed a commit to the repository a **Job** is executed and verifies the good shape of the code.

Last year Jenkins introduced the pipelines, a file in the repository that configures each step of the build. But even after a year of the release is hard to find some nice documentation and examples of how to use it. So I just wanted to share some tips.

### Jenkinsfile

Sometime you just need a simple file to understand how the system works.
