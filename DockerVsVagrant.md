[Index](./)
---
# Docker Vs Vagrant

##  Vagrant
Vagrant is a tool focused on providing a consistent development environment workflow across multiple operation systems. 

##Docker
Docker is a container management that can consistently run software as long as a containerization system exists.

##Meaning...
They solve two different problems. Vagrant provisions hosts on which to run things, whether it be a local vm or a remote host. Docker creates containers on a host, but doesn't provision hosts. Docker is an application that runs things (containers) and exposes them on a network, whether it is on one or many hosts.

* http://stackoverflow.com/questions/16647069/should-i-use-vagrant-or-docker-for-creating-an-isolated-environment

"It isn't correct to directly compare Vagrant to Docker. In some scenarios, they do overlap, and in the vast majority, they don't. Actually, the more apt comparison would be Vagrant versus something like Boot2Docker (minimal OS that can run Docker). Vagrant is a level above Docker in terms of abstractions, so it isn't a fair comparison in most cases.

Vagrant launches things to run apps/services for the purpose of development. This can be on VirtualBox, VMware. It can be remote like AWS, OpenStack. Within those, if you use containers, Vagrant doesn't care, and embraces that: it can automatically install, pull down, build, and run Docker containers, for example. With Vagrant 1.6, Vagrant has docker-based development environments, and supports using Docker with the same workflow as Vagrant across Linux, Mac, and Windows. Vagrant doesn't try to replace Docker here, it embraces Docker practices.

Docker specifically runs Docker containers. If you're comparing directly to Vagrant: it is specifically a more specific (can only run Docker containers), less flexible (requires Linux or Linux host somewhere) solution. Of course if you're talking about production or CI, there is no comparison to Vagrant! Vagrant doesn't live in these environments, and so Docker should be used.

If your organization runs only Docker containers for all their projects and only has developers running on Linux, then okay, Docker could definitely work for you!

Otherwise, I don't see a benefit to attempting to use Docker alone, since you lose a lot of what Vagrant has to offer, which have real business/productivity benefits:

* Vagrant can launch VirtualBox, VMware, AWS, OpenStack, etc. machines. It doesn't matter what you need, Vagrant can launch it. If you are using Docker, Vagrant can install Docker on any of these so you can use them for that purpose.
* Vagrant is a single workflow for all your projects. Or to put another way, it is just one thing people have to learn to run a project whether it is in a Docker container or not. If, for example, in the future, a competitor arises to compete directly with Docker, Vagrant will be able to run that too.
* Vagrant works on Windows (back to XP), Mac (back to 10.5), and Linux (back to kernel 2.6). In all three cases, the workflow is the same. If you use Docker, Vagrant can launch a machine (VM or remote) that can run Docker on all three of these systems.
* Vagrant knows how to configure some advanced or non-trivial things like networking and syncing folders. For example: Vagrant knows how to attach a static IP to a machine or forward ports, and the configuration is the same no matter what system you use (VirtualBox, VMware, etc.) For synced folders, Vagrant provides multiple mechanisms to get your local files over to the remote machine (VirtualBox shared folders, NFS, rsync, Samba [plugin], etc.). If you're using Docker, even Docker with a VM without Vagrant, you would have to manually do this or they would have to reinvent Vagrant in this case.
* Vagrant 1.6 has first-class support for docker-based development environments. This will not launch a virtual machine on Linux, and will automatically launch a virtual machine on Mac and Windows. The end result is that working with Docker is uniform across all platforms, while Vagrant still handles the tedious details of things such as networking, synced folders, etc.

To address specific counter arguments that I've heard in favor of using Docker instead of Vagrant:

* "It is less moving parts" - Yes, it can be, if you use Docker exclusively for every project. Even then, it is sacrificing flexibility for Docker lock-in. If you ever decide to not use Docker for any project, past, present, or future, then you'll have more moving parts. If you had used Vagrant, you have that one moving part that supports the rest.
"* It is faster!" - Once you have the host that can run Linux containers, Docker is definitely faster at running a container than any virtual machine would be to launch. But launching a virtual machine (or remote machine) is a one-time cost. Over the course of the day, most Vagrant users never actually destroy their VM. It is a strange optimization for development environments. In production, where Docker really shines, I understand the need to quickly spin up/down containers.
* I hope now its clear to see that it is very difficult, and I believe not correct, to compare Docker to Vagrant. For dev environments, Vagrant is more abstract, more general. Docker (and the various ways you can make it behave like Vagrant) is a specific use case of Vagrant, ignoring everything else Vagrant has to offer.

In conclusion: in highly specific use cases, Docker is certainly a possible replacement for Vagrant. In most use cases, it is not. Vagrant doesn't hinder your usage of Docker; it actually does what it can to make that experience smoother. If you find this isn't true, I'm happy to take suggestions to improve things, since a goal of Vagrant is to work equally well with any system."

## Opinionated Summary
(i.e. This applies to my scenario - it may well not apply to yours...)

The production environment is your main deployment target. It mostly means that you should only use Docker if your hosting provider has some sort of built-in support already for it, e.g. AWS EBS/ECS, GKE, etc. If you're deploying directly on EC2 or some other kind of VPS then just go with Vagrant, which is more development-oriented and easier to manage.
