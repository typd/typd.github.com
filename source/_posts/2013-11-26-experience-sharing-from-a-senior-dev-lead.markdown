---
layout: post
title: "Experience sharing from a senior dev lead"
date: 2013-11-26 22:41
comments: true
categories: 
---

A senior dev lead of my company did a experience sharing to our office. Below are the highlights.

#Incidents

He titled himslef the "incident reporter", as he thinks this is an important role. Something he did for incidents

  - Monitor and be pro-active
  - Log events as the incident evolves
  - Post-mortem analysis and followup
    - Build better alerting, monitoring and tracking
    - Look for other failure signs
  - Fail blog

And he also mentioned after incident've happened, it's a good chance for you to go over the related log and find defects you didn't pay enough notice before.

#The service checklist, when building a new service

- Isolated, decomposed: do one thing, and do it right
- Documentation
  - API
  - Discoverable
  - Node list, deployment procedures
- Devable
  - Bootstrap procedure: as easy as possible
  - Dev env should be as closely to prod as possible
- Staging environment
- Load balancing / redundancy / self healing
- Fault tolerant: anything can fail
  - Infrastructure failures
    - disk, ram, network switches
    - DNS stability
    - data center failure (rack, power, network, disaster)
  - Software stack pattern failure
    - date bomb (leap year, leap second, cert expiration)
- Dependency slowness
- Auto start
- Automated deployment
- Automated tests
- Log management
  - logrotate
  - centeralized logging
- Self monitoring
  - heartbeat
  - machine monitoring
  - exception alerts (rate limit emails)
  - metrics (metricsd, graphite)

#Others

In early days, some star devs tend to be heroism. But that doesn't work well as company becomes mature. Some better practices as we've grown up

- Better documentation
- More communication
  - know what does each team focus
  - prioritize the projects based on all teams' needs
- Rotate dev among teams, balance the output and the underlying benefits

#And more thoughts on him

- Good attitude on work
- Logical thinking, right judgement, and good perception on tech.
- Absolutely smart. I have to say that's a gift not everyone has, or trainable.
