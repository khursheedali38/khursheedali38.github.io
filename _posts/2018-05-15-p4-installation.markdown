---
layout: post
title: "P4: Installation"
date: 2018-05-15 +07:20:39 +0530
categories: SDN
---

In this blog post we will be setting up P4 lang environment for getting started with programmable data planes. SDN allows for programmable control planes, on the contrary P4 allows for programmable data planes. This is helpful for many [reasons][p4adv].

Clone the following repository: [P4 lang][p4l] 

To build the virtual machine:
+ Install [Vagrant][vup] and [VirtualBox][vb]
+ `cd vm`
+ `vagrant up`
+ Log in with *username* `p4` and *password* `p4` and issue the command `sudo shutdown -r now`
+ When the machine reboots, you should have a graphical desktop machine with the required software pre-installed.

**Note:** You may be prompted to enter the username and password and it might not work, this is because the prompt is for ubuntu server. If you look at log file or your terminal, installation is still in progress. So don't panic. You can follow this issue which I raised [here][gitissuep4].

In next series of posts I will be dicussing about solutions to the exercises provided in the P4 tutorials. While you don't need to have any prior experience in P4 syntax and constructs, as I will be briefing on the bare minimum required for a particular exercise, however a brief idea of what P4 does might be necessary.

[p4l]: https://github.com/p4lang/tutorials
[gitissuep4]: https://github.com/p4lang/tutorials/issues/120
[p4adv]: https://www.networkworld.com/article/3163496/cloud-computing/what-p4-programming-is-and-why-it-s-such-a-big-deal-for-software-defined-networking.html
[vb]: https://virtualbox.org/
[vup]: https://vagrantup.com/
