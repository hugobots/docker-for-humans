<p align="center">
  <img src="./images/docker-logo.png" height="150" align="center" />
  <h1 align="center">Docker for Humans</h1>
  <p align="center">Befriend yourselves with the cute fish!</p>
  <p align="center">Docker could seem scary, it really isn't. I will try to unravel everything that you need to know about docker in this guide and help you utilize it better in your daily job.</p>
  <p align="center">
  	<a href="https://creativecommons.org/licenses/by/4.0/">
  		<img src="https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg" />
  	</a>
  	<a href="http://makeapullrequest.com">
  		<img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square" />
  	</a>
  	<a href="http://twitter.com/kamranahmedse">
  		<img src="https://img.shields.io/badge/author-kamranahmedse-blue.svg" />
  	</a>
  </p>
</p>

## Introduction

I am going to be giving a talk to a small user group here in Berlin titled "Stupidly Simple Docker" and despite being thousands of articles and guides out there on the topic, I thought it would be better if I accompany the talk with a little "dumbed-down" guide to help those not attending. In this article I am going to dumb it down a little and explain everything that a non-ops developer needs to know about docker. The article does not assume that you have any prior knowledge of docker or containers etc and by the end of this article you will be able to create your own docker images, push to repository, know how to use docker compose, how to communicate between the images, how to SSH into containers and run commands etc. So without further ado, let's get started.

## What is Docker?

Docker, in a nutshell, helps you develop deploy and run your applications in containers. Container is nothing but an isolated group of processes sharing the kernel and other resources of the host machine. A single machine can run several many containers without any conflicts, all sharing the same kernel. Docker is the "container engine" – a set of tools written in Golang to manage the containers lifecycle (more on this later).

It is worth noting that containers are not something introduced by docker; they have been there for ages. It was Google that launched [Process Containers](https://en.wikipedia.org/wiki/Cgroups) in 2006 which was designed for limiting, isolating and accounting the resource usage of a collection of processes. Later on Process Containers was renamed to cgroups and merged to Linux Kernel in 2.6.24. However it was the launch of docker in 2013 that jump started the revolution of using containers in the wild.

## Containerization vs Virtualization

Containerization and virutalization both provide isolation of the environment; the difference is how they provide this isolation. In virtualization, [hypervisor](https://en.wikipedia.org/wiki/Hypervisor) allows multiple virtual machines to run on a single host system; where every VM includes the full OS image. Since each VM includes the full operating system, it is slow to boot and could take lots and lots of space on the machine. However in containerization the kernel of the host machine is shared among the *containers* using the "container engine". And since the containers share the same kernel from the host machine, they are fast to bootup and are smaller in size.

![](./images/containers-vs-virtualization.png)

## Comparing Docker to Vagrant or Virtual Machine

Since Vagrant was quite famous at that time, let me compare vagrant here with docker. Vagrant uses the concept of virtualization that we discussed above. The picture below explains the workflow when you are using vagrant for an application.

![](./images/vagrant.png)

As you can see, when using vagrant, we have a virtual machine installed on our development machine and with the code there is a little block representing "Provisioning Scripts". With vagrant, we have to write a set of provisioning scripts that setup the virtual machine by installing all the required dependencies and preparing the environment for us to work on our local. This code along with the provisioning scripts is then pushed to any repository management service, for example GitHub. During the deployment to staging or producction, we have to run these provisioning scripts against the staging or production server to make it ready for the application to run.

The workflow for Docker looks quite different from Vagrant. The picture below presents the workflow for Docker

![](./images/docker.png)

Before we proceed to explain the workflow, let me clarify something here that docker itself uses Linux technologies for it to operation. But you might be wondering, how is it possible to use Docker on let's say Windows and Mac then? Well docker utilizes some workarounds to achieve that. There is a small virtual machine designed for docker to operation, called boot2docker, docker initializes this VM and all the containers then run on this virtual machine. However, for mac, in the latest version of dockerthere is no need for this virtual machine as the new Docker.app uses the native hypervisor.framework to run containers.

With that out of the way, let's look at the workflow now. As you can see there are three key parts to understand for docker i.e. `Dockerfile`, `Docker Image` and `Container`.

Docker gives you the ability to snapshot the OS into a shared image, and makes it easy to deploy on other Docker hosts. Locally, dev, qa, prod, etc: all the same image. Sure you can do this with other tools, but not nearly as easily or fast.

## Benefits of using Docker

![](./images/container-benefits.png)

