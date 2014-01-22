---
layout: post
title: "Non blocking pipe"
date: 2014-01-22 21:54
comments: true
categories: 
---

Met a problem of linux pipe from daily work, finally got me to write a small tool to get rid of it. Worth to note.

#Motivation

I've built a central logging system based on logstash. It looks like this, basically,

<br/>

![](/images/posts/2014-01-22/1.png)

<br/>

Then every program use logstash as a shipper to redirect its log into the broker, which is a redis as message queue. As this [blog](http://adam.heroku.com/past/2011/4/1/logs_are_streams_not_files/) recommended, treatting log as stream rather than files, linux pipe make it possible to guide the stream to anywhere easily.

    application | java -jar logstash.jar agent -f logstash.conf

The problem occurs when the redis was accidently down, causes

- Logstash blocked, which is a designed behavior of [logstash](http://logstash.net/docs/1.3.3/life-of-an-event). It says "dropping messages or unlimited queue lenght are both undesirable behavior", so simply leaves no option and get it blocked.
- Then caused upstream application blocked, too! This is done by OS after the pipe buffer is filled up. This is a more serious problem as it's not easy to change OS default behavior.

<!-- more -->

#Solution?

Two possible solutions

- Introduce a log file, start logstash as a independent service to monitor it. This is the opposed way of the above blog recommended. This brings unnecessary disk IO, and you may need other things to avoid the log file getting too big, etc.
- Make the pipe non-blocking. But how?

#How

After investigation, logstash doesn't provide non-blocking option, described as above, although it should be easy to do. Why not write one? Here's the result,

    application | non_blocking_pipe java -jar logstash.jar agent -f logstash.conf

"non_blocking_pipe" is a middleware to read input from upstream, and send to downstream. It uses a fixed size internal queue. If downstream becomes blocked or slower than upstream, just drop the messages and remain reading inputs. A sidenote, why not do "application | non_blocking_pipe | downstream", it's because the middle component has to own the downstream as a subprocess, in order to know if it's blocked.

[Code available here](https://github.com/typd/non-blocking-pipe).

