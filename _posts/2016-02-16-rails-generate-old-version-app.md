---
layout: post
title: Generate old rails app
tags: [rails]
---

Sometimes you might need to create an older version of rails app, perhaps to debug.
Instead of manually editing Gemfile and updating bundle ( which might actually not work ), here is how we can specify it

{% highlight bash %}
  rails _4.1.0_ new FooBar
{% endhighlight %}


This will create a 4.1 rails app

{% highlight bash %}
  rails _version_ new app_name
{% endhighlight %}

`_version_` can be any valid rails version
