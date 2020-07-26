
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




Transforming the roam markdown files into hugo post files, is quite easy to automate. Just a execute a couple of scripts that were already there from my integration with drone.io

```
  - name: transform to hugo markdown
    shell: bash
    run: |
      mkdir posts
      pip3 install -r transform/requirements.txt
      cd zip
      find . -name \*.md -exec python3 ../transform/blog.py -i {} -o ../posts/ \;
```

Booom Done!




Push to my other repository where I store my blog :)

that's the trickiest part, I suppose I could create a secret with my a ssh key that I only use for push to the repository, but I saw an github action already that instead uses github token. I will copy part of this action in my workflow. Thanks cpina for the code ^^ https://github.com/cpina/github-action-push-to-another-repository


  - First, we need to generate an github API token


      - Go to the Github Settings (on the right hand side on the profile picture)
      - On the left hand side pane click on "Developer Settings"
      - Click on "Personal Access Tokens" (also available at https://github.com/settings/tokens)
      - Generate a new token, choose "Repo". Copy the token.
  - Now we need to add this token as a secret in the repository:

      - Go to the Github page for the repository that you push from, click on "Settings"
      - On the left hand side pane click on "Secrets"
      - Click on "Add a new secret" and name it "API_TOKEN_GITHUB"
  - Now we can do a git clone with the token, and will allow us to do a a push as well.

Again all this code is a copy of the https://github.com/cpina/github-action-push-to-another-repository, just that I didn't want to delete anything, and that's why I am not using the action directly but just copying it.

```
  - name: push to my blog
    shell: bash
    env:
      API_TOKEN_GITHUB: ${{ secrets.API_TOKEN_GITHUB }}
    run: |
      git config --global user.email "kozko2001@gmail.com"
      git config --global user.name "kozko2001"
      git clone "https://$API_TOKEN_GITHUB@github.com/kozko2001/blog-hugo.git" "blog"
      echo "1"
      ls blog/
      echo "2"
      cp posts/* blog/content/posts/
      git -C blog/ add
      echo "3"
      git -C blog/ status
      git -C blog/ commit -m "add content from roam-export"
      git -C blog/ push
```


**Conclusions**

Github actions are nice and easy to use, they remind me a lot of droneCI, which you can build the steps with docker containers and use commands inside. Which is exactly what github actions does.

I understand this is a really nice feature, which is free and eases the use of CI/CD practices on more projects (specially small ones), and the abstraction of each step is just a docker container resonates really well in my head. 

But on the other hand, I just feel all the inovation brought by small and motivated open source projects, has been just ripped and copied. And with it a lot of motivation...
