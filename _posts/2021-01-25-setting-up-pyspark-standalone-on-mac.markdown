---
layout: post
title: "Setting up pyspark standalone on mac"
date: 2021-01-21 +12:50:39 -0500
categories:  Spark, python
tags: pyspark, install, python3
---

You all might have had heard about `spark` - A large scale distributed data processing framework. Often the bottlenecks faced when learning spark are due to incorrect installations or due to not being aware of the dependencies and the environment spark is working on. In this guide I will present quick and easy steps to have your spark applications running in standalone mode on mac. 

With `python2` heading toward maintenance mode in 2021, `python3` is the way to go ahead. So we will breakdown our guide into two steps:
+ Python setup
+ Spark setup

## Python setup
Your mac might have come preinstalled with python2 by default, you can check it by `$python --version`. However, to install python 3, we will use `homebrew`, a package installer for mac, as `npm` is for `nodejs`.

### Install Homebrew
```shell
shell$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### Add the homebrew path in your profile 

```shell
shell$ vi ~/.bash_profile
```

```shell
export PATH="/usr/local/opt/python/libexec/bin:$PATH"
```

```shell
shell$ source ~/.bash_profile
```

![output][paths]

### Install python

```shell
brew install python
```

Yay, so `python3` neatly installed.  Onto spark now.

# Spark setup

Download the latest tarball from [here][spark]

### Install pyspark
```shell
shell$ pip install pyspark
```

Notes:

+ *You should have pip installed if you have installed python from homebrew as above.*
+ *You need Java SE runtime also, generally you should have it installed, if not find it [here][java].*

All good you are up and running with all the installations neatly. Now just move to bin folder in your spark binaries and enter `$pyspark` as shown. 

Note that you would want to use `python3`, if you observe pyspark uses `python2` then you can change the `PYSPARK_PYTHON` variable to point to `python3`. You can do that as follows by adding it to your profile.

```shell
shell$ vi ~/.bash_profile
```

```shell
export PYSPARK_PYTHON=python3
```

```shell
shell$ source ~/.bash_profile
```
![output][pyspark]

[spark]: https://spark.apache.org/downloads.html
[java]: https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html
[pyspark]: /assets/pyspark3.png
[paths]: /assets/PATH.png