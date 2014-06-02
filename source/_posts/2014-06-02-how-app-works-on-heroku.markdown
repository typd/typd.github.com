---
layout: post
title: "How app works on heroku"
date: 2014-06-02 22:32
comments: true
categories: 
---

Heroku is a lead service in the Paas field. The [12 factor app](http://12factor.net/) is a good summarize of their experiences on how to build a service. Util I've read [this "how heroku works" spec](https://devcenter.heroku.com/articles/how-heroku-works), and deployed a service recently, now I know more or less how they achieve that.

> # Deploy

> - Applications consist of your source code, a description of any dependencies, and a Procfile.
> - Procfiles list process types - named commands that you may want executed.
> - Deploying applications involves sending the application to Heroku using git.
> - Buildpacks lie behind the slug compilation process. Buildpacks take your application, its dependencies, and the language runtime, and produce slugs.
> - A slug is a bundle of your source, fetched dependencies, the language runtime, and compiled/generated output of the build system - ready for execution.
> - Config vars contain customizable configuration data that can be changed independently of your source code. The configuration is exposed to a running application via environment variables.
> - Add-ons are third party, specialized, value-added cloud services that can be easily attached to an application, extending its functionality.
> - A release is a combination of a slug (your application), config vars and add-ons. Heroku maintains an append-only ledger of releases you make.

> # Runtime

> - Dynos are isolated, virtualized unix containers, that provide the environment required to run an application.
> - Your application’s dyno formation is the total number of currently-executing dynos, divided between the various process types you have scaled.
> - The dyno manager is responsible for managing dynos across all applications running on Heroku.
> - Applications with only a single web dyno sleep after one hour of inactivity by the dyno manager. Scaling to multiple web dynos will avoid this.
> - One-off Dynos are temporary dynos that run with their input/output attached to your local terminal. They’re loaded with your latest release.
> - Each dyno gets its own ephemeral filesystem - with a fresh copy of the most recent release. It can be used as temporary scratchpad, but changes to the filesystem are not reflected to other dynos.
> - Logplex automatically collates log entries from all the running dynos of your app, as well as other components such as the routers, providing a single source of activity.
> - Scaling an application involves varying the number of dynos of each process type.

# About heroku

- As a Paas, I think it's more friendly than Google App Engine. And the specs are good.
- No judgement on the stability, real service cost yet.
