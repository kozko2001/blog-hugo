
---
title: Recent awesome - dev blog
date: 2022-09-18 00:00:00
---
---

## Recent Awesome

Is similar to github trending page, but for items in awesome lists.



It's composed on two basic parts

1. Crawler: a job executed daily (using github actions?) to parse the awesome lists. The idea is to get some information as (awesome list, category in the list, link to the resource, date added to the list)
2. a simple webpage that could get the json and show you the lastest additions

### Crawler

First milestone is be able to get the for a sample awesome list (for example this: https://github.com/TheJambo/awesome-testing#readme) get each bullet point with the text,  the link and the category (if possible)

I am going to give a try to `mistune2` library, that apart from generating html from markdown, can get you the AST (Abstract Syntax Tree) from the markdown.

From here it should be easy to detect the bullet points that have a link and get them.

You can see the ugly code here https://github.com/kozko2001/awesome-list-crawler

##### Infrastructure

I am gonna use AWS:
1. Create and ECR (a place to store docker images)
2. Create a github action that each time I commit to the repository will push the image to the ECR (I have to be extra careful to create a user with just enough permissions to push there) see: useful tutorial -> https://aws.plainenglish.io/build-a-docker-image-and-publish-it-to-aws-ecr-using-github-actions-f20accd774c3
3. Have a lambda that will execute the docker image once a day -> and store the result into a public S3

For doing all the provisioning I will try to use CDK for python (first time!)