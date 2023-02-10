---
title: "Lightrun Logs - an Introduction"
chapter: true
weight: 2
---

# Lightrun Logs - an Introduction

In today’s world, whenever a developer issues a new software version and deploys it into production, the most prevalent way to understand the application’s behavior is based on log lines - pieces of telemetry which are defined during the development stage. 

In practice, these logs are never enough - we’ve all encountered cases of missing a very specific log line when trying to troubleshoot a production issue, then having to release a new hotfix version in order to add this log. Alternatively, if deploying to production just for the sake of telemetry is not an option, there's a need to reproduce the bug locally to better understand the application’s behavior - a manual, cumbersome endeavor. 

This has gotten even worse in recent years with microservices and literally thousands of different entities running in different languages and different clouds - local reproduction is sometimes practically impossible, and going through the full CI/CD pipeline just to add some logs can take a long while (especially if done repetitively while debugging).

Lightrun Logs are added to the application immediately, and start emitting information as soon as they are instrumented. In essence, it's similiar to releasing a hotfix without having to actually release the hotfix!

An important thing to note here is [our sandbox](https://lightrun.com/security/) - a core part of our IP - that allows this log insertion to happen safely. We'll see it in action in just a moment.
