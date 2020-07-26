
---
title: Github Actions
date: 2020-07-26 00:00:00
---


Github actions allow you to create workflows likes the one you can have in a ci/cd system

You can go to one of your repositories, click in actions, and then in clic
![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fkzk-personal%2FdPwdRfxor7.png?alt=media&token=6b3964c5-c580-4312-a5b7-f265056a4dd7)

and then in setup workflow my self ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fkzk-personal%2FK3yV-cqxV0.png?alt=media&token=e27cef5e-780e-4cde-87e1-39e8f72b7278)

Now you will have the whole control to create your workflow in an editor! you can see the workflow specification in https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

My small project is about updating my blog, with the content of my roam research notes. 


Basically there are some notes that have a special annotation `blog:: ` that I want to import them into my hugo static generated blog

HERE SHOULD GO A HAND DRAW ARCHITECTURE OF THE PROJECT!

So what do I need to make it work:

1. Execute an action every 1h
2. This action will execute my roam-export project and will download my whole roam database, for that I will need to store my password of roam in a secured way
3. Filter and transform this markdown files into actual markdown for hugo
4. Add this files to a second repository and push the changes.

Let's see if we can do it!


Execute every 1 hour:


```clojure

on:
  schedule:
  - cron:  '0 * * * *'
```




Store some secret in github

You can add the secrets in the github repository, you can see the documentation here https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets

![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fkzk-personal%2FZ-MHFreq9L.png?alt=media&token=9a5765f6-6ef6-4be4-8eee-5073c8dcb6db)

that's how the step for executing looks like
```
  - shell: bash
    env:
      ROAM_USERNAME: ${{ secrets.ROAM_USERNAME }}
      ROAM_PASSWORD: ${{ secrets.ROAM_PASSWORD }}
      ROAM_DATABASE: ${{ secrets.ROAM_DATABASE }}
    run: |
      cd export
      npm install
      node index.js
      

```

I got some problems on unzip the zip file in github actions, cause the file that you download from roam-research ahs something "wrong", it's just a warning but it just cancels the pipeline.

I had to do a lot of trial and error commits, which is kind of ugly, I did a bit of search if you could https://github.com/nektos/act I didn't set it up, but looks promising :)
