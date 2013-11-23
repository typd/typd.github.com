---
layout: post
title: "The 12-factor app, all angles about building a robust app"
date: 2013-11-04 23:41
comments: true
categories: 
---

Just read [The 12-factor app](http://12factor.net/), published by heroku, talked about all angles about how you should do and what you need to consider for building a robust app.

Software development, deployment are happening fast. So as the tool set is also changing fast. Developers exchange their tools and methodologies, but seems that's not enough. This is a useful spec to summarise not just tools to use, but the things to consider behind each part of an application.

My abstract notes here, without the unnecessary long sentences.

<!-- more -->

# Codebase

- Use version control
- There is always a one-to-one correlation between codebase and the app, but there will be many deploys of the app. A deploy is a running instance of the app.

# Dependencies

- Lib installed through a packaging system can be installed system-wide or vendoring/bundling
- Never relies on implicit existence of system-wide packages
  Declares all dependancies, completely and exactly, via a dependency declaration manifest.
  Use a dependency isolation tool.
- Never relies on system tools.
  E.g. curl, those tools should be vendored into the app.

# Config

- Requires strict separation of config from code
  - A test for it: whether the codebase could be made open source at any moment
  - This does not include internal app config, e.g. config/routes.rb
- Stores config in environment variables, because
  - easy to change between deploys without changing any code
  - little chance of them being checked into code repo accidentally
  - not language nor os standard

# Backing services

- Any service the app consumes over the network as part of its normal operation.
- The code makes no distinction between local and third party services

# Build, release, run

- A codebase is transformed into a deploy through 3 stages:
  - Build stage: converts a code repo into an executable bundle.
  - Release stage: takes the build and combines it with config.
  - Run stage: runs the app in the execution environment.
- Uses strict separation between the build, release, and run stages.
- Deployment tools typically offer release management tools, most notably the ability to roll back to a previous release.
- Every release should have a unique ID
- Runtime execution can happen automatically in cases such as a server reboot, or a crashed process being restarted. Therefore, the run stage should be kept to as few moving parts as possible.
- Builds are initiated by devs whenever new code is deployed. The build stage can be complex, because dev is driving it.

# Processes

- 12-factor processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service.
- Ram or disk of the process can be used as a brief, single-transaction cache. Never assumes anything cached in ram or disk will be available on a future request or job.
- No "sticky sessions": cache user session data in ram and expecting future requests from the same visitor to be routed to the same process. Recommend a datastore offers time-expiration, memcached or redis.

# Port binding

- Completely self-contained, does not rely on runtime injection of a webserver into the execution environment to create a web-facing service. The web app exports HTTP as a service by binding to a port

# Concurrency

- Processes are a first class citizen.
- Adding more concurrency is simple because: share-nothing, horizontally partitionable nature
- Should never daemonize or write PID files. But rely on OS's process manager to manage output streams, respond to crashed processes, and handle user-initiated restarts and shutdowns.

# Disposability

- Disposable: can be started or stopped at a moment's notice.
- Processes should strive to minimize startup time.
- Processes shut down gracefully when they receive a SIGTERM signal from the process manager.
- Processes should also be robust against sudden death.

# Dev/prod parity

- Gaps between development and production
  - time gap: may take days, weeks, months to go into production
  - personal gap: developer write code, ops deploy it
  - tools gap: developers may use nginx, sqlite, osx, production may use apache, mysql, linux
- Design for continuous deployment, to keep the gap small
  - time gap: may have it deployed fast after write code
  - personal gap: dev are closely involved in deploying and watching it's behavior in production
  - tools gap: make development and production as similar as possible
- Resists the urge to use different backing services between development and production, because there may be tiny incompatibilities, cause to pass tests in local but fail in production. The cost is high over the lifetime.

# Logs

- Logs are the stream of aggregated, time-ordered events.
- Never concern with routing or storage of log. Each running process writes its event stream, unbuffered, to stdout. In staging or production, each process' stream will be captured, collated and routed to final destinations. These destinations are not visible to or configurable by the app, but managed by the execution environment. (Logplex and Fluent can help)

# Admin processes

- Developers may often wish to do one-off tasks. These should be run in an identical env as the app. They run against a release, using the same code and config. Admin code must ship with application code to avoid synchronization issues.
- The same dependency isolation techniques should be used on all process types.
