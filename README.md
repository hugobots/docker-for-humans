# Stupid Simple Guide to Docker

I am going to be giving a talk to a small user group here in Berlin titled "Stupidly Simple Docker" and despite being thousands of articles and guides out there on the topic, I thought it would be better if I accompany the talk with a little "dumbed-down" guide to help those not attending. In this article I am going to dumb it down a little and explain everything that a non-ops developer needs to know about docker. The article does not assume that you have any prior knowledge of docker or containers etc and by the end of this article you will be able to create your own docker images, push to repository, know how to use docker compose, how to communicate between the images, how to SSH into containers and run commands etc. So without further ado, let's get started.

Docker, in a nutshell, helps you develop, deploy and run your applications in isolated environments called containers. Before we go on rambling about docker and containers, let's make sure that we have a good idea about containers, containerization and how it is different from virutalization.

## Containerization vs Virtualization

Containerization is *almost* same as virutalization in a sense that both provide an isolated environment on top of the host system to run your application. The difference however is how this isolated environment is provided. In virtualization, [hypervisor](https://en.wikipedia.org/wiki/Hypervisor) provides a full virtual machine to the guest; accompanied with a full OS image and its dedicated kernel. However in container the kernel of the host machine is shared among the containers using the "container engine". And since the containers share the same kernel from the host machine, they are fast to bootup and are smaller in size.
