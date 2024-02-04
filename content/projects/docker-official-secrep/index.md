---
title: 'Docker Official Images: Security Report'
author: 'Darius Weber'
date: 2024-02-04
image: /projects/docker-official-secrep/thumbnail.jpg
tags:
  - docker
  - security
  - aquaSec
  - python
  - github actions
badges:
  - docker
  - security
  - aquaSec
  - python
  - github actions
links: [ { url: https://github.com/ManticSic/docker-official-security-report, icon: fab fa-github } ]
socialShare: false
toc: false
---

For over a year now, I've been dealing a lot with security and compliance in our company. One major goal is to only use "trustworthy" software. But what does "trustworthy" mean?

Especially in the discussion about Docker images, it took us many exhausting hours to find out what "trustworthy" means to us.
Many of my dev colleagues were happy when we announced that they are allowed to use a total of 177 images without approval: all the [Docker Official Images][1]!

Yep... today we know better. The approval of these images didn't solve the problems of our developers, not even close. They need a set of images to swiftly recreate complex infrastructure without approval processes that took weeks. This includes components like databases, search engines, and identity providers. But many applications we use are not included in Docker's official images. For example, Postgres is included, but we rely on MSSQL and Oracle databases. Unlucky.

Okay, we have a set of approved images, almost none of which we use. So, what's the problem?

We approved them on the assumption that they meet our security and compliance standards. We made this assumption based on the description:
> The Docker Official Images are a curated set of Docker repositories hosted on Docker Hub.
> These images provide essential base repositories that serve as the starting point for the majority of users.
What we expected from this statement: well-maintained and secure images.

But I'm not sure if they fulfill our security and compliance standards. We have found several outdated images and some blog posts which indicate that they are much less secure than implied, for example, [Aqua Security's report][2]. But most of these reports are several years old. Are they still true?

This time I want to be sure and have some facts. That's why I started a small project.
Currently, it consists of a Python script to generate a GitHub Actions workflow, which scans almost all official images and collects some data about them. As soon as I have collected enough datasets, I will start with an evaluation. The results will be published in a separate blog post.

[1]: https://docs.docker.com/trusted-content/official-images/
[2]: https://blog.aquasec.com/docker-official-images
