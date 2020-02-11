---
title: "Drone IO"
author: "Jordi Coscolla"
date: 2017-05-13T21:32:22.564Z
lastmod: 2020-02-11T21:48:47+01:00

description: ""

subtitle: "Hey lately I have been experimenting again with a bit of all CI/CD systems, like Jenkins, GoCD and a new player that didn’t know about come…"

image: "/posts/2017-05-13_drone-io/images/1.png" 
images:
 - "/posts/2017-05-13_drone-io/images/1.png" 
 - "/posts/2017-05-13_drone-io/images/2.png" 
 - "/posts/2017-05-13_drone-io/images/3.png" 
 - "/posts/2017-05-13_drone-io/images/4.png" 


aliases:
    - "/drone-io-c2e675b0fe80"
---

Hey lately I have been experimenting again with a bit of all CI/CD systems, like Jenkins, GoCD and a new player that didn’t know about come up during the research of information.

Please, give a warm welcome drone.io to the CI/CD! Well… if you didn’t know them they were in town from 2014… so yes… a little late for the welcome!




![image](/posts/2017-05-13_drone-io/images/1.png)



The thing is, after reading a bit, I just felt in love with these guys. The idea behind of using dockers to build the pipeline is not new, but they encourage/force from the beginning and with the first test that I made it was very promising.

Some features to highlight.

*   **hosted or cloud**: You can have everything on a hosted server or don’t worry at all about the CI/CD infrastructure.
*   **Unix style**: the very deep idea of drone platform is the use of docker containers to build/deploy/notify/whatever, this way you don’t end with conflicting plugins (yes, Jenkins you suck at it) each step just do one thing and can not interfere with next step in the pipeline.
*   **Integration with repositories**: It’s pretty magical how once you configure the drone service you automatically get all the webhooks configured and all repos without doing nothing.

So if you are in hype-mode now, let’s start with how to install drone in a self-hosted way in a server and how to integrate with a github project.

### **Installation**

First we should create a new OAuth application on the github, and write down the Client and the secret strings for the login configuration on drone




![image](/posts/2017-05-13_drone-io/images/2.png)



Then a simple docker-compose.yml like
`version: &#39;2&#39;``services:  
  drone-server:  
    image: drone/drone:0.6  
    volumes:  
      - /srv/docker/drone:/var/lib/drone/  
    restart: always  
    environment:  
      - VIRTUAL_HOST=ci.allocsoc.net  
      - VIRTUAL_PORT=8000  
      - LETSENCRYPT_HOST=ci.allocsoc.net  
      - [LETSENCRYPT_EMAIL=kozko2001@gmail.com](mailto:LETSENCRYPT_EMAIL=kozko2001@gmail.com)  
      - DRONE_GITHUB=true  
      - DRONE_GITHUB_CLIENT=${DRONE_GITHUB_CLIENT}  
      - DRONE_GITHUB_SECRET=${DRONE_GITHUB_SECRET}  
      - DRONE_SECRET=${DRONE_SECRET}  
      - DRONE_ADMIN=kozko2001``drone-agent:  
    image: drone/drone:0.6  
    command: agent  
    restart: always  
    depends_on: [ drone-server ]  
    volumes:  
      - /var/run/docker.sock:/var/run/docker.sock  
    environment:  
      - DRONE_SERVER=ws://drone-server:8000/ws/broker  
      - DRONE_SECRET=${DRONE_SECRET}  
      - DRONE_DEBUG=true  
networks:  
  default:  
    external:  
      name: nginx-bridge`

And execute the command
`DRONE_GITHUB_CLIENT=$$CLIENT_HERE$$ DRONE_GITHUB_SECRET=$$SECRET_HERE$$   
DRONE_SECRET=SOME_SECRET_STRING_HERE docker-compose up`

And voilà! you can now visit your domain name click on login, and if everything has worked… see all your repositories with all the webhooks configured to execute your pipelines on each push or tag.




![image](/posts/2017-05-13_drone-io/images/3.png)



If you want to dive deeper in the installation of the drone.io follow the installation documents.

[Installation Overview](http://docs.drone.io/installation/)


Next steps are, well configure the pipelines and the commands you want to do for the automatic integration and deployment.

### Configure the pipeline

The jobs or pipelines in drone are configured on a file inside the repository (.drone.yml), meaning that the configuration file is versioned and also that different branches on the code can have different building and deploying process.

And here I get my revelation about how drone works and really catches me.




![image](/posts/2017-05-13_drone-io/images/4.png)



Drone works only by using docker containers, here is an **.drone.yml** example from the drone documentation page [here](http://docs.drone.io/getting-started/).
`pipeline:  
  backend:  
    image: golang  
    commands:  
      - go get  
      - go build  
      - go test``frontend:  
    image: node:6  
    commands:  
      - npm install  
      - npm test``notify:  
    image: plugins/slack  
    channel: developers  
    username: drone`

1.  First there is a by default step of getting the code from the branch that did the push/tag/deploy and creates a docker volume with the source code on the repo
2.  Then, you can use any image you want to modify the volume, in this case we use the node image to install dependencies and execute the unit tests.
3.  Finally, we use an image a message with the state of the build to the team channel.

How great is that? I mean it remembers me a lot about the Unix style of command lines, you can chain as much as you want but they will never interfere. And also they are not tools special for the drone itself, in the build step we are using the library/node image maintained by docker team.

Also, there not a lot of plugins (images prepared to be useful for drone pipelines) but enough to be more than usable.

[Plugins | Drone](http://plugins.drone.io/)


Finally, we can use a DinD image container (Docker inside docker), Where the same drone agent that built the image, is able to execute commands to the host docker, and deploy the new image after all test are green.
`pipeline:  
  deploy_scrapy:  
    privileged: true  
    image: docker:17.04.0-dind  
    volumes:  
      - /var/run/docker.sock:/var/run/docker.sock  
    commands:  
      - &#34;docker build -t docker-trend-scrapy .&#34;  
      - &#34;docker rm -f docker-trend-scrapy || true &#34;  
      - &#34;docker run -d  --name=docker-trend-scrapy --restart=always --network nginx-bridge -v /srv/docker/docker-trend-scrapy:/data docker-trend-scrapy&#34;  
    when:  
      branch: &#39;master&#39;`

If you want to figure out more information about how drone works and how to configure it, here is the project documentation page

[Drone Continuous Delivery](http://docs.drone.io/)
