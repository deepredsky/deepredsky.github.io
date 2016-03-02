---
layout: post
title: "fish shell alias, functions and autocomplete"
date: 2016-03-02
tags: [fish, shell]
categories: dev
---

I wanted to create an alias to `git` as `g`. Here is a simple alias in fish

{% highlight bash %}
alias g="git"
{% endhighlight %}

This is great, but I wanted this alias to behave differently based on args supplied or not.
If no args supplied it should just do `git status`. If an arg(s) is supplied it should pass it along to git.

Here is the second version

{% highlight bash %}
function g
    if count $argv > /dev/null
        git $argv
    else
        git status
    end
end
{% endhighlight %}

This works. but now I have lost autocompletion provided by fish, because fish is not aware that `g` is a wrapper for `git`. Newwer version of fish providers `--wraps` to handle it

{% highlight bash %}
function g --wraps=git
    if count $argv > /dev/null
        git $argv
    else
        git status
    end
end
{% endhighlight %}

Now i get a nice autocompletion for `g`.

In order to force me to use `g` instead of `git`, I wanted to alias git to shout at me. So I add it as an alias again.

{% highlight bash %}
alias git="echo NO WAY!"
{% endhighlight %}

This works and i get shouted at if i use `git`. Unfortunately, the new `g` function also shouts at me, making it unusable. However, I can tell fish to use unaliased version of the command in my function.
Here is the final version.

{% highlight bash %}
function g --wraps=git
    if count $argv > /dev/null
        command git $argv
    else
        command git status
    end
end
{% endhighlight %}

here is how it looks

![Custom git wrapper]({{site.url}}/images/custom-git-wrapper.png)
