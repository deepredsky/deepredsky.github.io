---
layout: post
title: Finding words from source code
date: 2016-03-28 00:00
categories: bash, grep, typing
---

Recently I switched to dvorak keyboard layout and have been practising on [10fastfingers.com] to regain my typing speed. They have a nice way of practising on custom texts and I wanted to practice on words related to my own projects in ruby.

Here is a way to generate list of all words longer than two characters from all ruby files, ignoring the `vendor` folder, limited to 1000 unique words ordered by frequency

```bash

find . -name '*.rb' -not -path './vendor/*' -print0 | xargs -0 cat | grep -o -E '[a-zA-Z]{2,}' | sort | uniq -c | sort -nr | head -500 | awk '{print $2}' | xargs

```

This can also be useful to see the most frequently used words in a source code. For example, following snippet will return most frequently used words in the project.

```bash

find . -name '*.rb' -not -path './vendor/*' -print0 | xargs -0 cat | grep -o -E '[a-zA-Z]+' | sort | uniq -c | sort -nr | head -50

```

Same piping technique can be used to get most frequently used commands.

```bash

history | awk '{print $1}' | sort | uniq -c | sort -nr | head -50

```

![History]({{ site.url }}/images/history-screenshot.png)

I often use this to evaluate what cammands I use most frequently. I have added aliases for most frequently used commands like `git` and `bundle`.

[10fastfingers.com]: http://10fastfingers.com
