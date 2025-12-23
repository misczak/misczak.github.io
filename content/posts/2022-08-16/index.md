---
categories:
- Talks
- Cloud Security
date: "2022-08-16T00:00:00Z"
description: A lightning talk about connecting to complex, distributed architectures
  using only Private Endpoints and VPC/VNET Peering.
img_path: /assets/img/posts/20220816
pin: false
tags:
- MongoDB
- AWS
- Azure
- Security
- Networking
title: 'MongoDB World 2022 Talk: Look Ma, No Public IP!'
url: posts/mongodb-world-2022-talk-look-ma-no-public-ip
---

<style type="text/css" rel="stylesheet">
    .youtube-wrapper {
    position: relative;
    width: 100%;
    height: 0;
    padding-bottom: 56.25%;
  }
  .youtube-wrapper iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border: 0;
  }
</style>

Disclaimer: I am a MongoDB employee, and this is a lightning talk I gave at [MongoDB World 2022](https://www.mongodb.com/world-2022).

As your application continues to grow and scale, you may choose to take advantage of powerful MongoDB Atlas features, such as multi-region clusters and sharding, in order to provide a good user experience. While these features are useful, they can also introduce complexities to your application’s architecture if configured incorrectly. In this session, we’ll look at common architectures when designing multi-region sharded clusters and walk through how MongoDB Atlas allows your team to securely connect to each of the clusters without exposing unnecessary components to the public internet.

{{< youtube DQb63kSfqSY >}}