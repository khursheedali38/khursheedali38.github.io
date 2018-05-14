---
layout: post
title: "Jekyll Installation"
date: 2018-02-12 21:31:39 +0530
categories: jekyll
---

While jekyll installation isn't really complicated as it seems, people do encounter errors, most common of them being `permission denied`. One way to circumvent it is to run `sudo` command for installation, but that's not the safest option. You need to install it using root user which can be done via rvm installation. Following is the step by step guide to installation.

Usually it's the first part of installation, (i.e) installing `Ruby` and `RubyGems` via `RVM` which seems complicated, so we will look into that only, however I will provide link for later steps in installation as well. Those should be pretty easy.

+ Assuming you are on ubuntu or any linux distribution, firstly you need to install Ruby, so verify the RSA fingerprint

{% highlight ruby %}
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB 
{% endhighlight %}

+ Install it completely using 
`\curl -sSL https://get.rvm.io | bash -s stable --ruby.`

+ Once done with that, load the rvm into your shells 
source 
    + `~/.rvm/scripts/rvm` 
    + `rvm | head -n 1`


+ If installation is successful you should see the following output
 `rvm is a function`.

+ Now we need to install `RubyGems`, probably it should be pre-loaded into ubuntu, nevertheless you can follow it [here][rubygems], it's fairly simple.

+ Finally, follow the quickstart guide to carry forward your first blog post [here][post]. That should be self explanatory.

[rubygems]: https://rubygems.org/pages/download
[post]: https://jekyllrb.com/docs/quickstart/