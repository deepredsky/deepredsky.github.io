---
layout: post
title: switching to fish shell
date: 2016-03-20 17:13
tags: [fish, shell]
categories: dev
---

Here is how to switch your default shell to fish shell

1. Install fish

{% highlight bash %}
brew install fish
{% endhighlight %}

2. Switching to fish shell

{% highlight bash %}
chsh -s `which fish`
{% endhighlight %}

You might get an error like this.

{% highlight bash %}
chsh -s /usr/local/bin/fish
Changing shell for johndoe.
Password for johndoe:
chsh: /usr/local/bin/fish: non-standard shell
{% endhighlight %}

It's because the fish shell is not in `/etc/shells`. Adding the fish shell will fix this problem.
