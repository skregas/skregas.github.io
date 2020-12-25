---
layout: post
title: "Connecting up to Docker"
tags: [Docker, containers, learning]
---

Seems everyone knows about Docker. (if you are one of the lucky few, head on over to [docs.docker.com](https://docs.docker.com) and get sailing!)
It's a set of software tools to build containers of applications, packaging up related dependencies, programs, tools and other software, and deploying those containers, either througha DevOps pipeline through test and production, or to other developers on your team to get them up and running quickly. All they need is Docker installed!

Recently I've taken on a project at work to containerize (is there a better verb?) the app we've been building and testing over the last year. Other team members have dabbled in Docker, but there is very little in-house help available. Hello Internet!

I've spent the last few weeks learning the ins and outs of Docker basics, learning first-hand the weird quirks of writing a Dockerfile. One of the highlights was the understanding of context, or how the Docker engine sees the world. In similar fashion to any program, docker needs to be told, explicitly, how to structure the container supporting your app.

Getting into docker-compose and refining the build steps using the FROM ... AS ... syntax. The effect is smaller containers, as only the build steps that changed get rebuilt; the other layers remain untouched and get reused from cache. 

Finished [this](https://www.youtube.com/watch?v=fqMOX6JJhGo) beginners tutorial; now working through the Docker certification prep course using "Docker Essential Training" on lynda.com and setting up the labs on my local machine using VirtualBox. Investigating minimal Linux images to reduce load on the host and be able to run multiple guests at once. 