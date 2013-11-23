---
layout: post
title: "the right way of logging"
date: 2013-11-06 22:19
comments: true
categories: 
---

After read the 12-factor app spec, I took a close look to the logging section. For an application, it feels so nature to write logs to a file. But I just feel something isn't right.

- Do I need a cleaner tool like log rotate, or just pretend they're small forever?
- To debug something, I'm just forced to ssh across ocean and use a crappy vim on the host to find something weird.

"Elephant in the room". Until I read [this post](http://adam.heroku.com/past/2011/4/1/logs_are_streams_not_files/) in the spec, things become clear. Now here's my understanding.

<!-- more -->

The application log looks like a stream, and then it should be a stream. We normally append it to a file, just because that's the most obvious way of treating it. But it's defenitly not the only way. In fact for logging, the application's duty is done once it outputs to the stream. The logic of handling (append, rotate, clean) files, should (or say "can") not be a part of the application.

But what to do then if the application doesn't handle the log stream output. It's actually easier and more robust to take it out. Tools like Unix pipe, and [logstash](http://logstash.net/) or [fluend](https://github.com/fluent/fluentd) are more good at it than any application side logging lib.

For simple file logging, you can use

    $ mydaemon >> /var/log/mydaemon.log

For distributed logging,

    $ mydaemon | logger

Or still want a log file

    $ mydaemon | tee /var/log/mydaemon.log | logger

The "logger" is a placeholder for tools like logstash, which can be assembled into any kind of pipe line easily. Logstash has [doc](http://logstash.net/docs/1.2.2/) and [cookbooks](http://cookbook.logstash.net/). Just choose the input, output, filter as you need.

A typical setup may be:

    log stream
    => shipper: send log through udp out of the host
    => message queue: redis, mongodb, etc.
    => parser: parse each line to get timestamp, attributes, etc. May ingest parse logic here
    => elastic search: build index according to the parse result
    => web ui: for centralized viewing, querying, alerting, etc.

Move the elephant out of the room.
