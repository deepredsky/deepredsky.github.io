---
layout: post
title: TodoBackend Benchmarks
tags: [rails, elixir, sinatra, expressjs, nodejs, maru, phoenix, ruby, rails5]
---

I compared some of the framworks on [TodoBackend](http://todobackend.com/) project with some tweaks. 

All these are backed by `postgres`. So obviously these benchmarks are not purely for the framework itself but the whole stack.

# Phoenix

[https://github.com/jeffweiss/todobackend-phoenix](https://github.com/jeffweiss/todobackend-phoenix){:target="_blank"}

{% highlight bash %}
wrk -t20 -c100 -d30S --timeout 2000  "http://localhost:3000/api/todos"
Running 30s test @ http://localhost:3000/api/todos
  20 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    23.76ms    3.25ms 114.35ms   96.11%
    Req/Sec   212.01     16.17   252.00     80.19%
  126864 requests in 30.09s, 82.27MB read
Requests/sec:   4216.04
Transfer/sec:      2.73MB
{% endhighlight %}

# Sinatra

[https://github.com/moredip/todo-backend-sinatra](https://github.com/moredip/todo-backend-sinatra){:target="_blank"}

- removed the logging

{% highlight bash %}
wrk -t20 -c100 -d30S --timeout 2000  "http://localhost:3000/todos"
Running 30s test @ http://localhost:3000/todos
  20 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    13.63ms   11.83ms 173.18ms   88.35%
    Req/Sec   324.15    119.35   690.00     70.84%
  106624 requests in 30.10s, 93.75MB read
Requests/sec:   3542.85
Transfer/sec:      3.12MB
{% endhighlight %}

# ExpressJs

[https://github.com/dtao/todo-backend-express](https://github.com/dtao/todo-backend-express){:target="_blank"}

Non Cluster mode

{% highlight bash %}
wrk -t20 -c100 -d30S --timeout 2000  "http://localhost:3000/"
Running 30s test @ http://localhost:3000/
  20 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    81.96ms   97.83ms 498.72ms   79.26%
    Req/Sec   144.97     93.23   540.00     63.28%
  81397 requests in 30.10s, 44.48MB read
Requests/sec:   2704.28
Transfer/sec:      1.48MB
{% endhighlight %}

Cluster mode

- added cluster mode

{% highlight bash %}
wrk -t20 -c100 -d30S --timeout 2000  "http://localhost:3000/"
Running 30s test @ http://localhost:3000/
  20 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    21.58ms   20.51ms 408.22ms   90.05%
    Req/Sec   273.38     58.89   550.00     73.69%
  163169 requests in 30.07s, 89.16MB read
Requests/sec:   5425.57
Transfer/sec:      2.96MB
{% endhighlight %}

# Elixir Maru

[https://github.com/whitfieldc/maru_todo](https://github.com/whitfieldc/maru_todo){:target="_blank"}

{% highlight bash %}
wrk -t20 -c100 -d30S --timeout 2000  "http://localhost:3000/tasks"
Running 30s test @ http://localhost:3000/tasks
  20 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    21.77ms    5.43ms 143.73ms   95.62%
    Req/Sec   232.93     23.00   272.00     88.08%
  139189 requests in 30.07s, 68.25MB read
Requests/sec:   4628.15
Transfer/sec:      2.27MB
{% endhighlight %}

# Vanilla Rails

[https://github.com/hammerdr/todo-backend-rails](https://github.com/hammerdr/todo-backend-rails){:target="_blank"}

{% highlight bash %}
wrk -t20 -c100 -d30S --timeout 2000  "http://localhost:3000"
Running 30s test @ http://localhost:3000
  20 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    61.33ms   16.54ms 247.46ms   76.96%
    Req/Sec    60.09     32.24   141.00     60.18%
  26936 requests in 30.08s, 24.30MB read
Requests/sec:    895.37
Transfer/sec:    827.20KB
{% endhighlight %}

# Rails 5

{% highlight bash %}
wrk -t20 -c100 -d30S --timeout 2000  "http://localhost:3000"
Running 30s test @ http://localhost:3000
  20 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    41.48ms   27.82ms 417.76ms   65.79%
    Req/Sec    90.61     63.23   280.00     63.91%
  29777 requests in 30.10s, 26.16MB read
Requests/sec:    989.23
Transfer/sec:      0.87MB
{% endhighlight %}
