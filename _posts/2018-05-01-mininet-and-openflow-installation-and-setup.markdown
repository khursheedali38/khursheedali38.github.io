---
layout: post
title: "Mininet and OpenFlow: Installation and Setup"
date: 2018-05-01 23:47:39 +0530
categories: SDN
---

In this blog post I will walk you through the setup and installation to get started with SDN. In the upcoming posts I will introduce you to OVS and much more terminologies so that you can go ahead and experiment.

While you can find more elaborated and detailed instructions [here][of], I will however try to summarize the steps below. Note that, the instructions are for linux distributionsn such as ubuntu. Things should more or less similar in windows with *PuTTY* in effect for shell like interface.

1. Download and install [Oracle Virtual Box][ova].
2. Download the [Mininet VM image][mininetvm].
3. Import the mininet VM image in Oracle Virtual Box `File >> Import Appliance`.

The next few steps can be done on the linux shell to get more flexibility such as copy/paste and scrolling options which you might not get if you are doing in VM ubuntu server. To do it this way, *ssh* as follows `ssh -X mininet@192.168.56.101`.

3. Enter the username *mininet* and password *mininet*.
4. Check if your VM is connected to the internet `ifconfig -a`.
![output][net]

5. One of the interface in the above image connects to the internet, should be `eth1`. So make the interface public via *DHCP* `sudo dhclient eth1`. This will be useful later for setting up OVS for experimentation.
6. All set and you are good to go `sudo mn`.
![output][start]

Once you are done and up here, you are good to experiment with openflow and its working. However, you may want to work at the kernel level on switches, such as OVS, for your research. Follow my next blog post for OVS setup and working.

[of]: https://github.com/mininet/openflow-tutorial/wiki
[ova]: https://www.virtualbox.org/wiki/Linux_Downloads
[mininetvm]: https://github.com/mininet/mininet/wiki/Mininet-VM-Images
[net]: /assets/im1.png
[start]: /assets/im2.png