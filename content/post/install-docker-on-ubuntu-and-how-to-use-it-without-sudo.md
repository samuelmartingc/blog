+++
title = "Installing Docker on Ubuntu and how to use it without sudo"
description = "Installing Docker on Ubuntu and how to use it without sudo"
tags = [
    "development",
    "docker",
]
date = "2016-10-30"
categories = [
    "Development",
]

image = "docker-logo.png"

toc = true # optional, When set to TRUE this parameter, table of contents appears in only this article.
+++

Maybe you have heard about **Docker**, used to package your applications and services into a standardized unit which can be shipped and executed easily in every environment without external dependencies.
In this post I want to show you how to install Docker on **Ubuntu 16.04 LTS** in an easy way, and also how to run it without root privileges. Sounds right? Let’s start.


**Introduction**

Developing complex enterprise applications can be tedious when you must mount every external service needed in your new machine, Elastic Search, MongoDB, Rabbitmq, etc.
A good way to manage this task is by using Docker. With this container service you can easily download or create small containers with all the services you could need. Also it's essential to quickly deploy your code into production.


**Installing Docker on Ubuntu 16.04**

I'll make this guide as simple as I can. I will use Ubuntu 16.04 [LTS]. You will need the 64 bit version and your kernel must be at least in _3.10_, you can check this typing (uname -r) in the shell.

You must type the following commands in your shell, if you have any doubts you can see the official guide in https://docs.docker.com/  

```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
```

Write the following line in  /etc/apt/sources.list.d/docker.list
deb https://apt.dockerproject.org/repo ubuntu-xenial main


You can open a simple editor like nano with this command:

    sudo nano /etc/apt/sources.list.d/docker.list
    
And then paste the following text in the file and save it
```bash
sudo apt-get update
sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual
sudo apt-get install docker-engine
sudo service docker start
```

Excellent, you have installed Docker in your computer, you can check it typing
```bash
sudo docker run hello-world
```
If the installation has been a success, you will see _“Hello from Docker!”_



**Running Docker without requiring root permissions:**

Running Docker with sudo all time is not a great idea. We will fix this in this step :)
*Warning: in sensitive servers, we shouldn't be abe of running docker as any normal user*

First, we must create the docker group:
```bash
sudo groupadd docker
```
Then, add your current user to the docker group:
```bash
sudo gpasswd -a ${USER} docker
```
Now you can restart the Docker daemon:
```bash
sudo service docker restart
```
Now you should be able to run it without sudo:
```bash
docker run hello-world
```
If you have any problem, try logging out/in or rebooting your machine.




**Conclusion**


Now you can use Docker in your machine, it's very handy, if you haven’t use it yet, more than you can expect by now.
I hope this post has been helpful to you to install Docker.
